# 一个用C++11实现的简单易用的轻量级网络编程框架
平台|编译状态
----|-------
Linux | [![Build Status](https://travis-ci.org/xiongziliang/ZLToolKit.svg?branch=master)](https://travis-ci.org/xiongziliang/ZLToolKit)
macOS | [![Build Status](https://travis-ci.org/xiongziliang/ZLToolKt-build_for_mac.svg?branch=master)](https://travis-ci.org/xiongziliang/ZLToolKt-build_for_mac)
iOS | [![Build Status](https://travis-ci.org/xiongziliang/ZLToolKt-build_for_ios.svg?branch=master)](https://travis-ci.org/xiongziliang/ZLToolKt-build_for_ios)

## 项目初衷
多年的编程经历让我接触过多种网络开源库，譬如libevent、libev、libuv、boost.asio等等。这些开源框架有些是用C语言开发的，里面包含了各种难以阅读层层嵌套佶屈聱牙的宏，学习起来非常费力；有些使用起来又不甚方便，代码被切割成碎片零零碎碎；有些虽然使用简单，但是却非常宏大，牵涉各种代码，配置复杂，很难交叉编译。由于作者既从事过linux服务器编程又有jni、ios的编程经历，所以一直以来在寻求既能在服务器端高效运行又能在嵌入式平台方便开发的方法，但是一直没有找到比较合适的方案；于是作者大约在一年前开始整理多年的工作成果积累，抽取经过时间检验证明稳定有效的代码并且参考其他成熟的框架形成了这个项目。后面在我使用该项目（初期版本）用于实际开发，一路林林总总遇到了很多问题，但是在后面几个月不间断的调试、测试、修正、优化等过程中项目代码逐渐沉淀稳定，经过长时高强度的测试之后我把代码提交到github形成了这个项目。

## 特性
- 网络库
  - tcp/udp客户端，接口简单易用并且是线程安全的，用户不必关心具体的socket api操作。
  - tcp服务器，使用非常简单，只要实现具体的tcp会话（TcpSession类）逻辑,使用模板的方式可以快速的构建高性能的服务器。
  - 对套接字多种操作的封装。
- 线程库
  - 使用线程实现的简单易用的定时器（AsyncTaskThread）。
  - 读写锁。
  - 信号量的封装（ios下用条件变量实现）。
  - 自旋锁。
  - 线程组。
  - 简单易用的线程池，可以异步或同步执行任务，支持functional 和 lambad表达式。
- 工具库
  - 文件操作。
  - std::cout风格的日志库，支持颜色高亮、代码定位、异步打印。
  - INI配置文件的读写。
  - 监听者模式的消息广播器。
  - 基于智能指针的循环池，不需要显式手动释放。
  - 环形缓冲，支持主动读取和读取事件两种模式。
  - mysql链接池，使用占位符（？）方式生成sql语句，支持同步异步操作。
  - 简单易用的ssl加解密黑盒，支持多线程。
  - 其他一些有用的工具。
 
## 后续任务
- 提供更多的示例代码

## 编译(Linux)
- 我的编译环境
  - Ubuntu16.04 64 bit + gcc5.4(最低gcc4.7)
  - cmake 3.5.1
- 依赖
  - cmake：
	
    ```
    # 安装cmake
    sudo apt-get insatll cmake
    ```
  - libmysqlclient（使能ENABLE_MYSQL宏，非必备项）

    ```
    # 安装mysql客户端开发套件
    sudo apt-get install libmysqlclient-dev
    ```

  - libssl（使能ENABLE_OPENSSL宏，非必备项）

    ```
    # 安装openssl开发套件
    sudo apt-get install openssl
    sudo apt-get install libssl-dev
    ```
- 编译
  
  ```
  cd ZLToolKit
  mkdir -p build
  cd build
  cmake ..
  make
  make install
  ```  
    
## 编译(macOS)
- 我的编译环境
  - macOS Sierra(10.12.1) + xcode8.3.1
  - Homebrew 1.1.3
  - cmake 3.8.0
- 依赖
  - Homebrew

    ```
    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    ```
  - cmake
 
    ```
    brew install cmake
    ```
- 编译
  
  ```
  cd ZLToolKit
  mkdir -p build
  cd build
  cmake ..
  make
  make install
  ```
	 
## 编译(iOS)
- 编译环境和依赖:`请参考macOS的编译指导。`
- 编译
  
  ```
  cd ZLToolKit
  mkdir -p build
  cd build
  #IOS_PLATFORM宏可以选择：OS(默认,真机)/SIMULATOR(32位模拟器)/SIMULATOR64(64位模拟器)
  cmake .. -DCMAKE_TOOLCHAIN_FILE=../iOS.cmake -DIOS_PLATFORM=OS
  make
  ```
- 你也可以生成Xcode工程再编译：

  ```
  cd ZLToolKit
  mkdir -p build
  cd build
  # 生成Xcode工程，工程文件在build目录下
  cmake .. -DCMAKE_TOOLCHAIN_FILE=../iOS.cmake -DIOS_PLATFORM=SIMULATOR64 -G "Xcode"
  ```
	
## 联系方式
- 邮箱：<771730766@qq.com>
- QQ群：542509000


