# 程序崩溃拦截模块（暂时只支持Win7）
这个项目目前还是雏形，暂时只支持win7。本人会继续维护下去。

# 群号码：963718093 开源交流群，加群一起学习共同进步。
[![.Net Core 开源学习交流](http://pub.idqqimg.com/wpa/images/group.png ".Net Core 开源学习交流")](http://shang.qq.com/wpa/qunwpa?idkey=d42b97a72adbb99729c59fc68173df53093e6d8908dd4588f2d81907a84d8f3b)

# 博客园地址：https://www.cnblogs.com/hanjunjun-blog

## 这个项目用到的语言
>```
>1.C#、C++、win32汇编
>理论上这个模块能支持任何语言开发的程序。
>```

## 应用场景
>```
>这个模块是模仿了QQ产品崩溃错误报告的UI，功能和它类似，qq每个产品根目录下都会有一个BugReport.exe，用来上传腾讯产品崩溃的dmp文件，让开发人员可以不断的完善产品。
>try只能拦截语言层面的异常，有些异常是语言拦截不到的，比如空指针引用，内存溢出，这些就需要用这个模块去拦截。
>```

## 模块使用方法
>```c#
>[DllImport("BugReportLib.dll", EntryPoint = "SetGlobalExceptionFilter", SetLastError = true, CharSet = CharSet.Ansi, ExactSpelling = false, CallingConvention = CallingConvention.StdCall)]
>        public extern static void SetGlobalExceptionFilter(int timeTick, string productName);
>        static void Main(string[] args)
>        {
>                SetGlobalExceptionFilter(15, "C#测试程序");
>                Console.WriteLine("加载BugReportLib.dll成功！");
>                Console.ReadLine();
>            }
>    
>    只需要在程序的起始位置，调用一下接口，就可以实现崩溃的拦截
>    ```

## 1.项目结构
>```
>├─dist					项目编译输出目录
>├─Document				文档
>│  └─x86注入工具		 主动使程序崩溃的注入工具
>└─src					
>    ├─BugReport			错误报告UI
>    │  ├─Common
>    │  ├─lib
>    ├─BugReportLib		崩溃拦截模块
>    │  ├─build			
>    ├─DotNetTest		C#窗体测试程序
>    └─PythonTest		Python窗体测试程序
>```

## 2.开发环境配置

* 工程建议使用vs2019打开
* 安装net framework 4.0
* 安装PyCharm python开发工具

## 3.项目编译

> C#的比较简单直接重新生成整个解决方案即可。
> python的需要编译成exe，命令如下：
> pyinstaller ctest.py

##  4.Demo演示

> 这边演示的是C#在win7下崩溃拦截的步骤
1.
![步骤一](https://raw.githubusercontent.com/HanJunJun/BugReport/master/Document/images/1.png)

2.
![步骤二](https://raw.githubusercontent.com/HanJunJun/BugReport/master/Document/images/2.png)

> python的也是一样的步骤。不过要先把py代码编译成exe