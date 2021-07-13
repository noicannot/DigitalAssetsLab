## bufio

### 前言

---

​	流工具包，提供了读取器和写入器的对象创建和一些工具方法。

----

一，包介绍

```go
// Package bufio implements buffered I/O. It wraps an io.Reader or io.Writer
// object, creating another object (Reader or Writer) that also implements
// the interface but provides buffering and some help for textual I/O.

包bufio实现缓冲I/O。它包装一个io.Reader或io.Writer
实现了接口实现的对象
接口，但为文本I/O提供缓冲和一些工具

defaultBufSize=4096  //默认的bufsize

```

二，Reader 结构

```go
// Reader implements buffering for an io.Reader object.
type Reader struct {
	buf          []byte
	rd           io.Reader // reader provided by the client
	r, w         int       // buf read and write positions
	err          error
	lastByte     int // last byte read for UnreadByte; -1 means invalid
	lastRuneSize int // size of last rune read for UnreadRune; -1 means invalid
}
io.Reader 接口对象
error 接口对象，实现了Error() string 的对象
```

> 用来存储读取内容的 buf  []byte 对象，io.Reader 读取器 ，读取位置和写入位置，错误信息对象。

```go
// NewReaderSize returns a new Reader whose buffer has at least the specified
// size. If the argument io.Reader is already a Reader with large enough
// size, it returns the underlying Reader.
func NewReaderSize(rd io.Reader, size int) *Reader {
	// Is it already a Reader?
	b, ok := rd.(*Reader)
	if ok && len(b.buf) >= size {
		return b
	}
	if size < minReadBufferSize { //minReadBufferSize=16
		size = minReadBufferSize
	}
	r := new(Reader)
	r.reset(make([]byte, size), rd)
	return r
}

// NewReader returns a new Reader whose buffer has the default size.
func NewReader(rd io.Reader) *Reader {
	return NewReaderSize(rd, defaultBufSize)
}
// Reset discards any buffered data, resets all state, and switches
// the buffered reader to read from r.
func (b *Reader) Reset(r io.Reader) {
	b.reset(b.buf, r)
}
func (b *Reader) reset(buf []byte, r io.Reader) {
	*b = Reader{
		buf:          buf,
		rd:           r,
		lastByte:     -1,
		lastRuneSize: -1,
	}
}
```

> 如果 rd已经是一个Reader 直接进行解包，如果size小于16更新为16，并生成Reader对象
>
> Reset(r io.Reader)  重置一个io.Reader 对象的读取器buf []byte
>
> NewReader 方法是一个接口，可以进行自定义读取。比如混淆。

```go
func TestReaderSimple(t *testing.T) {
	data := "hello world"
	b := NewReader(strings.NewReader(data))
	if s := readBytes(b); s != "hello world" {
		t.Errorf("simple hello world test failed: got %q", s)
	}

	b = NewReader(newRot13Reader(strings.NewReader(data)))
	if s := readBytes(b); s != "uryyb jbeyq" {
		t.Errorf("rot13 hello world test failed: got %q", s)
	}
}
```

>一个测试读取器和一个自定义混淆读取器。下面我来看看它的实现吧。

```go
// Reads from a reader and rot13s the result.
type rot13Reader struct {
	r io.Reader
}

func newRot13Reader(r io.Reader) *rot13Reader {
	r13 := new(rot13Reader)
	r13.r = r
	return r13
}

func (r13 *rot13Reader) Read(p []byte) (int, error) {
	n, err := r13.r.Read(p)
	for i := 0; i < n; i++ {
		c := p[i] | 0x20 // lowercase byte
		if 'a' <= c && c <= 'm' {
			p[i] += 13
		} else if 'n' <= c && c <= 'z' {
			p[i] -= 13
		}
	}
	return n, err
}
```

>Read方法进行了混淆读取。
