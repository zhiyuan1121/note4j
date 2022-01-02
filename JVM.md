### jvm的基础概念jvm，是一个虚拟机，java之所以能跨平台是因为java是编译成class文件之后在jvm上去运行的。所以java代码的运行不依赖与平台（系统）只依赖与jvm。

jvm运行的是class文件，只要能编译成class文件的代码jvm都能运行，并不只能运行java这一种语言。

### 类的加载（创建Class对象）

java类是通过ClassLoader来进行加载的。类的加载过程是双亲委派，先判断自己是否加载过若没有加载传递给父加载器去判断。父加载器判断的过程中发现加载过就直接返回；若顶级父加载器（c++实现的）也没有加载就尝试加载，无法加载传递给子加载器。若子加载器无法加载报错；

双亲委派的实现是ClassLoader抽象类中的模板方法loadClass，若要打破双亲委派在自定义classloader的之后重写改方法即可。

classLoader的父加载器并不是继承的而是类中的一个属性 “parent” 

#### java自带的ClassLoader有三个

1.用c++实现的classLoader（这个类在java代码中是不存在的）  

2.ExtClassLoader

3.AppletClassLoader

#### 自定义classLoader

自定义classLoader需要继承ClassLoader若要延用双亲委派只需重写findClass方法即可，读取需要加载的文件调用defineClass进行类的加载。（百度实现细节）

应用场景：代码加密，对正常编译的class文件进行加密，甚至可以修改后缀名，在自定义类加载器进行解密加载。

打破双亲委派的应用场景，热编译。模板方法中的双亲委派同一个class只能加载一次无法实现热编译。

### 解释还是编译

jvm默认是混合执行模式即有解释也有编译。执行频率较高的热点代码会编译执行，其余代码为解释执行。可以设置虚拟机参数做成只编译或只解释执行。

### 垃圾回收

#### 回收算法

#### G1

