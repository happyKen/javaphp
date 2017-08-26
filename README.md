
---------------
# php和java通信工具的搭建

</br>

## 工具简述

 php-java-bridge：一个连通php和java的工具，这是它的官网介绍： 
 
The PHP/Java Bridge is an implementation of a streaming, XML-based network protocol, which can be used to connect a native script engine, for example PHP, Scheme or Python, with a Java virtual machine. It is up to 50 times faster than local RPC via SOAP, requires less resources on the web-server side. It is faster and more reliable than direct communication via the Java Native Interface, and it requires no additional components to invoke Java procedures from PHP or PHP procedures from Java.

</br>

## 下载地址

[php-java-bridge](http://php-java-bridge.sourceforge.net/pjb/download.php)



</br>


## 版本环境

 内容 | 版本
 ---  | ---
PHP版本 | 最高为5.4,当前测试为5.4/5.3
JDK | 官方最新版本,当前测试为1.8
php-java-bridge | 官方最新版本,当前测试为6.2.1
操作系统 | Windows7 32位/64位或者Linux(Centos6.5)


</br>


## 安装使用 

### 第一步：安装 
1. JDK的安装：正常安装即可，并配置好环境变量
2. PHP的安装：正常安装即可
3. php-java-bridge的安装： 
* 先下载Java服务器Tomcat正常安装，安装好后，开启Tomcat服务器
* 将下载的php-java-bridge包放到webapps下面
* 等待Tomcat执行解析，会在该目录下面生成相同名字的文件夹
* 将该文件夹拷贝到Apache服务器下面使用 
*(*注*：网上的教程可以正常使用，调用java系统函数和简单的jar包，但是对于复杂的jar包会遇到各种各样的问题，所以建议使用这种方式)


### 第二步：使用
1. 不需要开启Tomcat(最好关闭掉)，开启apache服务器，双击运行javabridge.jar,选择8080端口 
(javabridge.jar也需要放到java虚拟机下面，参见下面第二点规则)。
2. 尽可能的将jar包放到java虚拟机下面，即jre安装下面(比如：C:\Program Files\Java\jre1.8.0_20\lib\ext)
3. 在PHP文件中不需要再引用jar包，因为放到虚拟机下面去了，java会自动调用 
(注：第1点中的javabridge.jar是在第一步:安装中第3点中获得的)


</br>


## 注意事项



### 函数使用：
1. 高版本的java_require不再使用,也无法使用,由于放到java虚拟机下面,则不需要再手动引入包文件 
2. java_value()用于获取值,而且必须使用该函数获取值  
(特别注意：如果该值需要存入数据库，那么必须使用该java_value函数,不然会报错，或者无法存入数据库) 
3. java_inspect()对实例化或者方法进行print_r类似的输出 
(注：请不要直接使用var_dump这样的输出方法输出java的类、方法、变量，需要使用java_inspect或者java_value，例如：var_dump(java_inspect($abc))) 
4. 实例化使用 $test = new Java("Test")的方式,如果实例化的方法中存在参数,可以这样new Java("Test","pram") 



### 注意事项：
1. 务必确保对java.inc的引用，确保引用正确 
2. 务必确保对jar包放在能引用的地方，比如java虚拟机jre下面 
3. 在PHP中调用Java使用PHP的的写法即可 

