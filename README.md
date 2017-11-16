# Note_Java_Android_零散知识点





--命名规范--

1.驼峰形式   fileName
2.包名小写   com.libratone
3.类名首字母大写，之后驼峰   UserForm
4.组件  功能+组件   mloginButton
5.变量  mxxx       mUser
6.静态常量   全部大写  _ 分割     public static final int START_FLAG_REDELIVERY = 0x0001;
7.Public -> Protect -> Private
8.静态变量 -> 实例变量 -> 构造器 -> 方法  （类中） 


//================================================================================//


--注释规范--

  类 、方法   规范如下：
/**
 *@author     作者
 *@since      从哪个版本开始加入的
 *@version    当前修改是在哪一个版本上
 *@Time 	     当前修改时间
 *@see        说明当前的作用是什么
 *@param      解释所有参数意义
 *@return     解释返回值意义
 *@exception  是否抛出异常，并解释
*/

  变量        规范如下：

/*xxxxxxxxxxxxxxxxxxxxxxx*/  解释当前变量意义

//   方法中，某行 ，注解


//===========================================================================================================================//


例如：

/**
 *@author     Eminem
 *@since      v1.0
 *@version    v2.2.2
 *@Time 	     2017/01/11 11:30:00
 *@see        说明当前的作用是什么
 *@param      解释所有参数意义
 *@return     解释返回值意义
 *@exception  是否抛出异常，并解释
*/

public class ChangeColor{

   /* 红色颜色值  */ 
   public static final int RED_COLOR_VALUE= 0x0001;

   /*  当前颜色  */ 
   private Color mColor;

  /**
   *@author     Eminem
   *@since      v1.0
   *@version    v2.2.2
   *@Time 	2017/01/11 11:30:00
   *@see        改变颜色
   *@param      当前颜色值
   *@return     改变后的颜色值
   *@exception  null
   */

   public Color changeColor(Color color){

     ……

  }

  /**
   *@author     Eminem
   *@since      v1.0
   *@version    v3.5
   *@Time 	2017/02/22 11:30:00
   *@see        改变颜色
   *@param      frontColor 前置颜色，  backColor ，后置颜色
   *@return     改变后的颜色值
   *@exception  null
   */

   protect Color changeColor(Color frontColor,Color backColor){

     ……

  }

}


//===========================================================================================================================//


1：jvm 基于 栈，用指令操作   代码编译后生成.class文件

dalvik 优化于jvm 为了使用内存 性能 较低的手机等设备， 基于 寄存器 ， 代码先编译成.class文件，再转成.dex文件执行

一个应用，一个虚拟机实例，一个进程（所有android应用的线程都是对应一个linux线程，都运行在自己的沙盒中，
不同的应用在不同的进程中运行。每个android dalvik应用程序都被赋予了一个独立的linux PID(app_*)）

进程就是一个应用程序在处理机上的一次执行过程，它是一个动态的概念，而线程是进程中的一部分，进程包含多个线程在运行。

（app A,app B,  A/B 就是2个进程对于Linux，A/B可以有N个线程做不同事情）


//===========================================================================================================================//


2：Activity  onStart / onStop  (activity 是否可见)   onResum / onPause (activity 是否处于前台)   # 先可见->在前台->不在前台->不可见

A activity  ->  B activity  生命周期： A (onPause)->B (onCreat)->B (onStart)->B (onResum)->A (onStop)->A (onDestroy)


//===========================================================================================================================//


3：avtivity 被异常停止时候  才回调用 onSaveInstanceState()  / onRestoreInstatncaeState() 这两个方法。在onSaveInstanceState() 保存想要的数据，onRestoreInstatncaeState() / onCreate() 均可 恢复数据；官方推荐在onRestoreInstatncaeState() 恢复数据。

# 系统会自动 保存 视图结构的数据，类似 切后台再回来，界面数据还在，（委托模式 ，一级一级保存数据）

生命周期：onPause / onSaveInstanceState()  (两者无先后顺序一说)->onStop()->onDestroy()->onCreate()->onStart()->onSaveInstanceState()


//===========================================================================================================================//


栈  ：  操作系统 分配的 内存中一段连续地址，用来存储一些临时数据，速度略低于寄存器

堆  ：  在内存中动态生成的树状结构的内存地址，用来存储 持久化的数据，不释放容易内存溢出（java 有GC帮助回收）


成员变量、局部变量、静态变量的区别 ：

 
           	    成员变量				 局部变量				  静态变量


定义位置   	  在类中,方法外      	 	  方法中,或者方法的形式参数   			 在类中,方法外

初始化值	  有默认初始化值	       	  无,先定义,赋值后才能使用  			有默认初始化值

调用方式	    对象调用				   ---					对象调用，类名调用

存储位置	      堆中			           栈中					  方法区

生命周期          与对象共存亡                         与方法共存亡                              与类共存亡



在一个类中，如果一个变量能够用来描述一个类的属性，那就定义为成员变量，否则，它就应该定义为局部变量。
而如果一个变量在全局中都能使用（某个内容是被所有对象所共享），那么我们就可以把这个变量用static来修饰，即为静态变量。



//===========================================================================================================================//



	                          --抽象  接口  ，抽象接口--


如果我们对于问题领域的理解是：AlarmDoor在概念本质上是Door，同时它有具有报警的功能。我们该如何来设计、实现来明确的反映出我们的意思呢？前面已经说过，abstract class在Java语言中表示一种继承关系，而继承关系在本质上是"is a"关系。所以对于Door这个概念，我们应该使用abstarct class方式来定义。另外，AlarmDoor又具有报警功能，说明它又能够完成报警概念中定义的行为，所以报警概念可以通过interface方式定义。如下所示：
	abstract class Door {
		abstract void open();
		abstract void close()；
	}
interface Alarm {
	void alarm();
}
class AlarmDoor extends Door implements Alarm {
	void open() { … }
	void close() { … }
   	void alarm() { … }
}
这种实现方式基本上能够明确的反映出我们对于问题领域的理解，正确的揭示我们的设计意图。其实abstract class表示的是"is a"关系，interface表示的是"like a"关系，大家在选择时可以作为一个依据，当然这是建立在对问题领域的理解上的，比如：如果我们认为AlarmDoor在概念本质上是报警器，同时又具有Door的功能，那么上述的定义方式就要反过来了。




抽象接口 ：设计了一个接口，但实现这个接口的子类并不需要实现接口中的全部方法，也就是说，接口中的方法过多，对于某些子类是多余的，我们不得不浪费的写上一个空的实现。

/*
    假设有一个顶层接口
*/
public interface ITestInterface{
    void method1();
    int method2();
    boolean method3();
}


/*
    抽象类abstract实现了ITestInterface顶层接口
*/

public abstract class TestAbstract implements ITestInterface{
    //找出接口中必要的方法，也就是子类必须实现的方法，定义成抽象方法，交由子类实现
    public abstract void method1();
    public abstract int method2();
    
    //一些独特的方法可以在抽象类中默认实现
    public boolean method3(){
        return true;
    }
}


/*
    普通类TestClass1继承了TestAbstract抽象类
*/

public class TestClass1 extends TestAbstract{
    
    //TestClass1必须实现抽象的method1方法，该方法最早是接口中定义的
    public void method1(){
        
    }
    //TestClass1必须实现抽象的method2方法，该方法最早是接口中定义的
    public int method2(){
        return 1;
    }
    
    //接口中的method3方法对于TestClass1无关紧要，因此不做重写。
}


/*
    普通类TestClass2继承了TestAbstract抽象类
*/

public class TestClass2 extends TestAbstract{
    
    //TestClass2必须实现抽象的method1方法，该方法最早是接口中定义的
    public void method1(){
    
    }
    //TestClass2必须实现抽象的method2方法，该方法最早是接口中定义的
    public int method2(){
        return 2;
    }
    
    //method3方法对于TestClass2来说至关重要，因此必须重写。
    public boolean method3(){
        return false;
    }
    
}



//===========================================================================================================================//


Android Studio 2.2   CMake  来开发NDK



利用Java位运算符，完成Unsigned转换。

       正常情况下，Java提供的数据类型是有符号signed类型的，可以通过位运算的方式得到它们相对应的无符号值，参见几个方法中的代码：

      public int getUnsignedByte (byte data){      //将data字节型数据转换为0~255 (0xFF 即BYTE)。
         return data&0x0FF;
      }

      public int getUnsignedByte (short data){      //将data字节型数据转换为0~65535 (0xFFFF 即 WORD)。
            return data&0x0FFFF;
      }       

     public long getUnsignedIntt (int data){     //将int数据转换为0~4294967295 (0xFFFFFFFF即DWORD)。
         return data&0x0FFFFFFFFl;
      }


//===========================================================================================================================//



	  
	 Android  ANR  adb 不显示log的时候  可以去 "/data/anr/traces.txt"这个目录，查找死机的原因
	 
	 
//===========================================================================================================================//



	 Android Studio使用Wifi调试的方法：使用ADB WIFI

	（http://blog.csdn.net/liduolp/article/details/51545144）


OTG :是On-The-Go的缩写，是近年发展起来的技术,主要应用于各种不同的设备或移动设备间的联接，进行数据交换。

Android USB Host(Android USB 主机通讯)
http://blog.csdn.net/wizardmly/article/details/8350137


//===========================================================================================================================//

Hash，一般翻译做“散列”，也有直接音译为”哈希”的，就是把任意长度的输入（又叫做预映射，pre-image），通过散列算法，变换成固定长度的输出，
该输出就是散列值。这种转换是一种压缩映射，也就是，散列值的空间通常远小于输入的空间，不同的输入可能会散列成相同的输出，
而不可能从散列值来唯一的确定输入值。


MD4(RFC1320)是MIT的RonaldL.Rivest在1990年设计的，MD是MessageDigest的缩写。
它适用在32位字长的处理器上用高速软件实现--它是基于32位操作数的位操作来实现的。

MD5(RFC1321)是Rivest于1991年对MD4的改进版本。它对输入仍以512位分组，其输出是4个32位字的级联，
与MD4相同。MD5比MD4来得复杂，并且速度较之要慢一点，但更安全，在抗分析和抗差分方面表现更好。

MD5是一种不可逆的加密算法，目前是最牢靠的加密算法之一，尚没有能够逆运算的程序被开发出来，
它对应任何字符串都可以加密成一段唯一的固定长度的代码。

SHA1是由NISTNSA设计为同DSA一起使用的，它对长度小于264的输入，产生长度为160bit的散列值，因此抗穷举(brute-force)性更好。
SHA-1设计时基于和MD4相同原理,并且模仿了该算法。SHA-1是由美国标准技术局（NIST）颁布的国家标准，
是一种应用最为广泛的hash函数算法，也是目前最先进的加密技术，被政府部门和私营业主用来处理敏感的信息。
而SHA-1基于MD5，MD5又基于MD4。

CRC的全称为CyclicRedundancyCheck，中文名称为循环冗余校验。
它是一类重要的线性分组码，编码和解码方法简单，检错和纠错能力强，在通信领域广泛地用于实现差错控制。

Hash算法在信息安全方面的应用主要体现在以下的3个方面：

 1)文件校验
 2)数字签名
 3)鉴权协议

//===========================================================================================================================//

Android gradle productFlavors   产品特性
 
 签名 打包 分组 ····
 
 http://blog.csdn.net/crazyman2010/article/details/53471162
 
 不同渠道依赖不同库
 http://www.jianshu.com/p/9b50c4059d61
 
