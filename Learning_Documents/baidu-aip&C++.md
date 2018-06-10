# baidu-aip&C++
> 本文档用以记录通过C++调用baidu-aip实现基本应用的详细步骤
---
# 下载项

* [openssl]()
* [curl]()
* [json]()
* [Nasm]()
* [ActivePerl]()

---
# 安装项
* ActivePerl:
> 选择典型安装即可，之后 next->next

* Nasm：
> 确定->next->next(改变路径的话记得添加path到环境变量)->install

---
# openssl编译
* 进入命令行模式（win+R->cmd）
* step1
```
$ cd /d E:\aip+c++\openssl-1.0.2m
$ perl Configure VC-WIN32 --prefix=E:\OpenSSL

```
> /d 后为包含openssl文件名的完整路径 <br>
> E:\OpenSSL为编译后的文件的存放路径，需要提前创建 <br>

![p1][pic1] <br>

* step2
```
$ ms\do_nasm

```

![p2][pic2]  <br>

* step3
```
$ cd /d F:\Visual Studio\VC\Auxiliary\Build
$ vcvars32.bat

```
> F:\Visual Studio\VC 为VS中的VC安装路径 <br>
> \Auxiliary\Build 为vcvars32.bat文件所在路径,也可能是\bin,注意查看下是否有 vcvars32.bat 这个文件 <br>

![p3][pic3]

* step4
```
$ cd /d E:\aip+c++\openssl-1.0.2m
$ nmake -f ms\ntdll.mak

```
> 需要一定的时间，请耐心等候

![p4][pic4]

* step5
> 测试生成的库是否正确
```
$ nmake -f ms\ntdll.mak test

```
> 杀毒软件可能会拦截此操作，执行此步骤时关闭杀毒软件
> 显示passed all tests说明库没有问题,执行下一步<br>

![p5][pic5]

* step6
```
$ nmake -f ms\ntdll.mak install

```
> 恭喜，你的openssl编译完成

![p6][pic6]

* 请在OpenSSL文件夹下查看你需要的文件
* 注意：
> 以上编译的是 release 版本，若要编译 debug 版，将上述第 2 步中的 VC-WIN32 改成 debug-VC-WIN32即可。<br>
> 若要编译静态库，则用 ms\nt.mak 替换掉上面用到的 ms\ntdll.mak 即可。<br>
---
# libcurl.lib编译
* 1.打开VS工程,路径：
> curl->projects\windows\VC15\curl-all.lsn <br>

* 2.修改Debug模式为DLL Release - DLL OpenSSL <br>
* 3.打开libcurl的属性： <br>
>> C/C++->常规->附加包目录->点击右边的倒三角->加入以下路径： <br>
```
 E:\libcurl-ssl\curl-7.60.0\include\openssl

```
>> C/C++->预编译器->预编译器定义->加入以下指令： <br>
```
NDEBUG;BUILDING_LIBCURL;USE_OPENSSL

```
>> 链接器->常规->附加库目录->加入以下路径： <br>
```
E:\OpenSSL\lib (包含libeay32.lib和ssleay32.lib)

```
>> 链接器->输入->附加依赖项->输入以下库名： <br>
```
ws2_32.lib
wldap32.lib
libeay32.lib
ssleay32.lib

```
* 4.直接编译，编译完成后会提示，找不到依赖项libeay32.dll和ssleay32.dll <br>
> 打开OpenSSl\bin,复制libeay32.dll和ssleay32 <br>
> 粘贴到：<br>
curl\build\win32\VC15\DLL Release - DLL OpenSSl <br>

* 5.对libcurl右键，点击重新生成，完成后再次编译项目就OK了
---

# Visual Studio工程配置
## 调用libcurl.lib编译前的准备
> 声明：先不考虑维护，将多数的头文件放在同一目录下

* 在项目的源文件(main.cpp)目录下创建include文件夹,复制以下文件粘贴到此文件夹下
> 有些文件可能不需要，但方便起见 Ctrl+A、Ctrl+V is OK <br>

> 1.复制curl\include\curl中的文件<br>
> 2.复制baidu-aip中的文件<br>
> 3.复制baidu-aip\base中的文件 <br>
> 4.复制json\include\json中的文件到<br>

* 复制相关文件到源文件目录

> 1.复制json\src\lib_json下的.cpp和json_valueiterator.inl、json_tool.h（jsoncpp.cpp可不要）<br>
> 2.curl\Build\Win32\...\ libcurl.dll <br>
> 3.编译后的openssl\lib\ libeay32.dll、ssleay32.dll <br>

* 复制文件到 __工程目录__ (.lsn)

> 三个lib库libcurl.lib、libeay32.lib、ssleay32.lib <br>
>> libcurl.lib在curl\Build\win32\DLL Release .. 中 <br>
>> libeay.lib和ssleay32.lib在编译后的openssl\lib中 <br>

## VS编译前相关设置

* 1.属性->C\C++ -> 预处理器->预处理器定义：添加

> BUILDING_LIBCURL;HTTP_ONLY

* 2.链接器->常规->附加库目录：

> project_path（三个lib库位置）

* 3.链接器->输入->附加依赖项：加入

>libcurl.lib;libeay32.lib;ssleay32.lib;
ws2_32.lib;winmm.lib;wldap32.lib
>>注意：分号相当于换行，不写分号就换行写

---

# 常见问题

* 无法打开PDB文件,勾选以下两项

> 1.工具->选项->调试->常规->启动源服务支持 <br>
> 2.调试->符号->Microsoft符号服务器


---

# 测试代码

[百度AI文字识别测试](code)

> 暂未开放，之后会加入到网站和github中 <br>



>LINKS:
>>[pic1]: https://raw.githubusercontent.com/LEIZI3V/git_repository/master/picture/1.PNG
[pic2]: https://raw.githubusercontent.com/LEIZI3V/git_repository/master/picture/2.PNG
[pic3]:
https://raw.githubusercontent.com/LEIZI3V/git_repository/master/picture/3.PNG
[pic4]:
https://raw.githubusercontent.com/LEIZI3V/git_repository/master/picture/4.PNG
[pic5]:
https://raw.githubusercontent.com/LEIZI3V/git_repository/master/picture/5.PNG
[pic6]:
https://raw.githubusercontent.com/LEIZI3V/git_repository/master/picture/6.PNG
[code]:
