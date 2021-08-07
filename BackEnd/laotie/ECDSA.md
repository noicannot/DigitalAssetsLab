## ECDSA算法

---

[toc]



![椭圆曲线算法](https://pic1.zhimg.com/v2-3a4252b86b3f16ec9eb38b2cc6e4e053_1440w.jpg?source=172ae18b)

### 一，什么是ECDSA算法

>ECDSA全称：**[Elliptic Curve Digital Signature Algorithm](https://link.zhihu.com/?target=https%3A//en.wikipedia.org/wiki/Elliptic_Curve_Digital_Signature_Algorithm)**  有兴趣的朋友可以去维基百科看看这个算法的算法原理。
>
>**椭圆曲线数字签名算法** 既然是签名算法，就不是用来加密的。也就是说数据是公开的，只是用来保护数据不被篡改。

> 签名本身将被分成两部分，称为`R`和`S`。为了验证签名的正确性，你只需要公钥（用私钥在曲线上面产生的点）并将公钥和签名的一部分`S`一起代入另外一个方程，如果这个签名是由私钥正确签名过的数字签名，那么它将给出签名的另外一部分`R`。简单来说，一个数字签名包含两个数字，`R`和`S`，然后你使用一个私钥来产生`R`和`S`，如果将公钥和`S`代入被选定的魔法数学方程给出`R`的话，这个签名就是有效的。仅仅知道公钥是无法知道私钥或者创建出数字签名。

> 通常`ECDSA`会总共使用160比特，它可以表示相当大的数，可以由49个数字在里面。

### 二，为什么要用签名算法

>大部分的时候我们都会拿AES算法来作比较。原因是AES是名副其实的加密算法。解密需要密钥。应用场景比如，用户的重要数据。密钥一般会存放于用户自己手里。但是密钥是这种算法的软肋。毕竟什么时候都需要用这个密钥才能解密。
>
>对应AES破坏性的加密算法，ECDSA椭圆曲线签名算法，是在不破坏数据的前提下，对数据进行签名。而签名是用来验证数据是否被篡改过。

### 三，基础原理和算法

> **模运算**：简单的说就是整数求余数。余数会在0~除数之间不断的变化。
>
> **Hash**: SHA1加密哈希，相对于模运算来说复杂的多的多，但是可以用模运算来解释。
>
> 由于SHA1产生Hash碰撞的可能性最低。所以如果想通过伪造数据来获取特定的hash是不可能的。

### 四，椭圆曲线密码学

![](https://www.zhihu.com/equation?tex=y%5E2+%3D+%28x%5E3%2Ba%5Ctimes+x+%2B+b%29+%5Cmod+p+%5C%5C)

> 根据公式我们能够看到y的取值范围是  0到(p-1). 

1. 通过以下的两个方式，我们可以通过随机的数做系数进行多少次以下的推导。

- 椭圆曲线的点加法
- 椭圆曲线的点乘法

2. 一个椭圆曲线乘法的特性是你有一个点![[公式]](https://www.zhihu.com/equation?tex=R%3Dk%5Ctimes+P)，你知道![[公式]](https://www.zhihu.com/equation?tex=R)和 ![[公式]](https://www.zhihu.com/equation?tex=P)，但是你无法据此求出![[公式]](https://www.zhihu.com/equation?tex=k)，因为这里并没有椭圆曲线减法或者椭圆曲线除法可用，你并不能通过![[公式]](https://www.zhihu.com/equation?tex=k%3DR%2FP)得到![[公式]](https://www.zhihu.com/equation?tex=k)。并且，因为你可以做成千上万次的加法，最终你只是知道在曲线上面结束的点，但是具体是如何到达这个点你也并不知道。你无法进行反向操作，得到与点![[公式]](https://www.zhihu.com/equation?tex=P)相乘以后给你点![[公式]](https://www.zhihu.com/equation?tex=R)的 ![[公式]](https://www.zhihu.com/equation?tex=k)

> 这种即便你知道原点和终点，但是无法知道被乘数是`ECDSA`算法背后安全性的所有基础，而这一原则也被称为**[单向陷门函数](https://link.zhihu.com/?target=https%3A//en.wikipedia.org/wiki/Trapdoor_function)**。

### 五，椭圆曲线算法

> 对于`ECDSA`算法，首先你需要知道你的曲线参数，一共有![[公式]](https://www.zhihu.com/equation?tex=a%2Cb%2Cp%2CN%2CG)，你已经了解![[公式]](https://www.zhihu.com/equation?tex=a)和 ![[公式]](https://www.zhihu.com/equation?tex=b)是曲线方程的参数（![[公式]](https://www.zhihu.com/equation?tex=y%5E2%3Dx%5E3%2Ba+%5Ctimes+x+%2B+b)）,![[公式]](https://www.zhihu.com/equation?tex=p)是模运算的底，![[公式]](https://www.zhihu.com/equation?tex=N)是曲线上面点的个数，对于`ECDSA`，还需要一个参数`G`，它表示一个你所选中的一个参考的起始点。它可以是曲线上面的任意一点。
>
> 验证一个签名并不是只知道公钥就可以。首先还必须知道这个公钥是从什么曲线参数推导出来的。
>
> 总结一下：首先，你有一对密钥：公钥和私钥，私钥是一个随机数，也是160比特大小，公钥是将曲线上的点![[公式]](https://www.zhihu.com/equation?tex=G)与私钥相乘以后的曲线上的点。令![[公式]](https://www.zhihu.com/equation?tex=dA)表示私钥，一个随机数，![[公式]](https://www.zhihu.com/equation?tex=Qa)表示公钥，曲线上面的一个点，我们有![[公式]](https://www.zhihu.com/equation?tex=Qa+%3D+dA+%5Ctimes+G)，其中![[公式]](https://www.zhihu.com/equation?tex=G)是曲线上面的参考点。

### 六，总结

> 产生一个签名的两个方程，![[公式]](https://www.zhihu.com/equation?tex=R%3Dk%5Ctimes+G) 和 ![[公式]](https://www.zhihu.com/equation?tex=S%3Dk%5E%7B-1%7D%28z%2BdA%5Ctimes+R%29+%5Cmod+p)，这些方程的强势在于实际上有一个方程里面有两个未知数（![[公式]](https://www.zhihu.com/equation?tex=k)和 ![[公式]](https://www.zhihu.com/equation?tex=dA))，因此你是无法确定其中的任意一个。
>
> 确保随机数![[公式]](https://www.zhihu.com/equation?tex=k)确实是随机产生的变得非常重要，并且没有人能够猜测、计算或者其它任何类型的攻击来得到随机数。
>
> `ECDSA`算法非常安全，不可能找到私钥。如果有办法很容易找到私钥，那么每台计算机、网站、系统的安全都可能受到危害，因为很多系统都依赖`ECDSA`来保证安全，而且不可能破解。



