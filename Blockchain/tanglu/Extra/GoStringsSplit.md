### 描述：strings.Split 函数用于将指定的分隔符切割字符串，并返回切割后的字符串切片。

### 语法：需要导入string包
strings.Split(s,sep)
参数         说明                         备注
s             待分割的字符串          字符串类型的参数
sep         分隔符                       字符串类型的参数

### 返回值：
返回一个字符串切片。

### 使用示例
Split()函数将字符串根据分隔符切割。切割后返回一个字符串切片，切片len（长度）和cap值(容量)等于原字符串中存在分隔符的数量+1（仅在s不是空字符串的情况下成立。）
切片拥有长度和容量。
切片的长度是它所包含的元素个数。
切片的容量是它的第一个元素开始数，到其底层数组元素末尾的个数。
切片s的长度和容量可通过表达式len(s)和cap（s）来获取。

代码：
package main
import (
    "fmt"
    "strings"
)
func main(){
      demo :="I&love&Go,&and&I&also&love&Python."
      string_slice := strings.Split(demo,"&")

      fmt.Println("result:",string_slice)
      fmt.Println("len:",len(string_slice))
      fmt.Println("cap:",cap(string_slice))
}
运行结果如下：
result:[I love Go,and I also love Python.]
len:8
cap:8


1.当分隔符不存在于原字符串中时，Split()函数将原字符串转换成一个len和cap值都为1的字符串切片。
2.当分隔符是空字符串时，Split()函数将字符串中的每一个字符分割成一个单独的元素。
3.当Split()函数的两个参数都是空字符串时（即s和sep都是空字符串），Split()函数返回一个len和cap值都为0的空字符串切片。
4.当s为空字符串，sep不为空字符串时，虽然得到的结果仍然是字符串切片，但是字符串切片的len和cap值是1。返回的结果是包含一个空字符串的字符串切片。
5.返回的字符串切片中不再包含分隔符
