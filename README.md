基于 dio 封装的网络请求框架
-------------
### 项目简介
    项目中基本会用到网络请求，flutter 中有 dio 网络请求框架项目地址：https://github.com/flutterchina/dio，
    而在实际开发中我们在请求的时候会添加一些头部信息和后台进行一些校验和一些公共信息的传递如版本号等，同时针对返回的
    信息我们会定义一套数据结构模版如前后台协同定义的状态码，如区分token失效等，所以在开发中我们需要对网络框架进行进
    一步的封装来达到统一处理类似切面编程的效果，同时对网络请求框架进行进一步封装之后也方便后期对网络请求框架的替换，
    因为在实际的使用中我们是可以不引用网络框架代码的。
    项目中添加来 bloc 框架的使用，使得页面和逻辑层相互独立，具体参考参考：https://www.jianshu.com/p/4d5e712594b4
### 使用方式
    1、在项目中的 pubspec.yaml 文件中添加 dio: 2.1.13 的支持，如果不需要json序列化可不添加json_serializable相
    关的库，依赖如下：
        dependencies:
          flutter:
            sdk: flutter
        
          cupertino_icons: ^0.1.2
          #网络请求库
          dio: 2.1.13
          #json序列化库 ：json_serializable
          json_annotation: ^2.0.0
          #bloc 框架使用时用到，不用到 bloc 框架的可不添加
          rxdart: ^0.19.0
        
        dev_dependencies:
          flutter_test:
            sdk: flutter
          #json序列化库 ：json_serializable
          build_runner: ^1.0.0
          #json序列化库 ：json_serializable
          json_serializable: ^2.0.0
    2、将本项目中 lib 下 http_util 包考进自己项目中
    3、在需要使用的地方导入 MyHttpUtil.dart、BaseResponse.dart、RequestListener.dart文件
    4、发送请求：
    //Post请求
    _sendPostRequest() {
        MyHttpUtil.instance.post(
            "musicBroadcastingDetails?channelname=public_tuijian_spring",
            RequestListener(
                onSuccessListener: (BaseResponse data) => _onResponseSuccess(data),
                onErrorListener: (BaseResponse errorData) => _onResponseError(errorData)
            )
        );
    }
    
    //Get请求
    _sendGetRequest() {
        MyHttpUtil.instance.get(
            "musicBroadcastingDetails?channelname=public_tuijian_spring",
            RequestListener(
                onSuccessListener: (BaseResponse data) => _onResponseSuccess(data),
                onErrorListener: (BaseResponse errorData) => _onResponseError(errorData)
            )
        );
    }
    5、如果需要添加请求头、拦截器，修改一些参数，在MyHttpUtil.dart中进行修改，参考备注
### 友情提示
    如果下载此项目在mac运行在ios设备上报 Podfile.lock 相关错误，尝试用终端进入到ios目录下执行 pod install 命令
    习惯安卓开发的朋友可能习惯来安卓 json 解析的方式，在 flutter 开发时候对 flutter json 解析可能一下不是很适应，
    因为 flutter json 解析需要额外做一些处理，可以参考下面这篇文章（在 Flutter 中解析复杂的 JSON）
    当然flutter也有一些开源库是针对 json 解的，如 json_serializable package，具体使用方法参考下面这篇文章（使用
    代码生成库序列化JSON），part 导入的时候名称要和文件名相同不然会运行 flutter packages pub run build_runner build 错误
[在 Flutter 中解析复杂的 JSON](https://github.com/xitu/gold-miner/blob/master/TODO1/parsing-complex-json-in-flutter.md)
[使用代码生成库序列化JSON](https://flutterchina.club/json/)
### demo 代码运行效果如下
  <img src="https://github.com/zhoujiulong/flutter_http_utils/blob/master/img/img_a.png?raw=true" width="30%"/>

