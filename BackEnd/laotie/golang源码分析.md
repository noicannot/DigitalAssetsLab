### Golang 源码分析-error

---

### Golang -源码分析

error/wrap.go

```go
// Unwrap returns the result of calling the Unwrap method on err, if err's
// type contains an Unwrap method returning error.
// Otherwise, Unwrap returns nil.
func Unwrap(err error) error{
	u, ok := err.(interface {
		Unwrap() error
	})
	if !ok {
		return nil
	}
	return u.Unwrap()
}
```

> 处理接口对象是否满足某个接口的断言。感觉减少了错误的出现。

```go
// Is reports whether any error in err's chain matches target.
// The chain consists of err itself followed by the sequence of errors obtained by
// repeatedly calling Unwrap.
// An error is considered to match a target if it is equal to that target or if
// it implements a method Is(error) bool such that Is(target) returns true.
// An error type might provide an Is method so it can be treated as equivalent
// to an existing error. For example, if MyError defines
//	func (m MyError) Is(target error) bool { return target == fs.ErrExist }
// then Is(MyError{}, fs.ErrExist) returns true. See syscall.Errno.Is for
// an example in the standard library.
func Is(err, target error) bool {
	if target == nil {
		return err == target
	}
	isComparable := reflectlite.TypeOf(target).Comparable()
	for {
		if isComparable && err == target {
			return true
		}
		if x, ok := err.(interface{ Is(error) bool }); ok && x.Is(target) {
			return true
		}
		// TODO: consider supporting target.Is(err). This would allow
		// user-definable predicates, but also may allow for coping with sloppy
		// APIs, thereby making it easier to get away with them.
		if err = Unwrap(err); err == nil {
			return false
		}
	}
}
```

```
Is reports whether any error in err's chain matches target.
报告err链中是否有错误与目标匹配。
The chain consists of err itself followed by the sequence of errors obtained by repeatedly calling Unwrap.
该链由err本身和通过反复调用Unwrap获得的错误序列组成。
An error is considered to match a target if it is equal to that target or if it implements a method Is(error) bool such that Is(target) returns true.
如果一个错误等于该目标，或者它实现了一个方法（错误）bool，那么（target）返回true，则认为该错误与目标匹配。
An error type might provide an Is method so it can be treated as equivalent to an existing error. For example, if MyError defines
错误类型可能提供Is方法，以便将其视为等效于现有错误。例如，如果MyError定义
func (m MyError) Is(target error) bool { return target == fs.ErrExist }
then Is(MyError{}, fs.ErrExist) returns true. See syscall.Errno.Is for an example in the standard library.
然后 Is（MyError{}，fs.ErrExist）返回true。有关标准库中的示例，请参见syscall.Errno.Is。
```

>判断发生的错误的类型，返回boolean。主要是实现过程，
>
>- 目标错误不能是nil
>- 反射获取目标错误的可比较状态
>- 错误依次拆箱，直到找到符合的目标错误。
>
>以后再高层的业务逻辑判断错误的时候，会考虑使用此方法来确定业务的具体错误进行有针对的返回错误。

除了Is方法外还有一个As方法：

```go
// As finds the first error in err's chain that matches target, and if so, sets
// target to that error value and returns true. Otherwise, it returns false.
// The chain consists of err itself followed by the sequence of errors obtained by
// repeatedly calling Unwrap.
// An error matches target if the error's concrete value is assignable to the value
// pointed to by target, or if the error has a method As(interface{}) bool such that
// As(target) returns true. In the latter case, the As method is responsible for
// setting target.
// An error type might provide an As method so it can be treated as if it were a
// different error type.
// As panics if target is not a non-nil pointer to either a type that implements
// error, or to any interface type.
func As(err error, target interface{}) bool {
	if target == nil {
		panic("errors: target cannot be nil")
	}
	val := reflectlite.ValueOf(target)
	typ := val.Type()
	if typ.Kind() != reflectlite.Ptr || val.IsNil() {
		panic("errors: target must be a non-nil pointer")
	}
	if e := typ.Elem(); e.Kind() != reflectlite.Interface && !e.Implements(errorType) {
		panic("errors: *target must be interface or implement error")
	}
	targetType := typ.Elem()
	for err != nil {
		if reflectlite.TypeOf(err).AssignableTo(targetType) {
			val.Elem().Set(reflectlite.ValueOf(err))
			return true
		}
		if x, ok := err.(interface{ As(interface{}) bool }); ok && x.As(target) {
			return true
		}
		err = Unwrap(err)
	}
	return false
}
```

```
As在err的链中查找与target匹配的第一个错误，如果是，则将target设置为该错误值并返回true。否则，返回false。
该链由err本身和通过反复调用Unwrap获得的错误序列组成。
如果错误的具体值可赋值给target所指向的值，或者错误的方法为（interface{}）bool，例如As（target）返回true，则错误与target匹配。在后一种情况下，As方法负责设置目标。
错误类型可能提供As方法，因此可以将其视为不同的错误类型。
如果target不是指向实现error的类型或任何接口类型的非nil指针，则As panics。
```

>其实只从代码的实现来看，我觉得这个方法就没有多少实用性，主要是动不动就panic 。毕竟我在处理错误现场呢，就是为了更加准确的判断是哪里出了错误，没必要再崩溃一次吧。。。

至此，errors/wrap.go就介绍完毕了。

### 总结

​	一直以来，我都有反射会大大降低代码的运行效率，但是今天看源码发现，也没有大大降低，这就看情况有没有必要了。如果我们在收拾残局，做程序的善后处理，你还关注效率吗？肯定不是，而是到底问题出在那里了。对不对？