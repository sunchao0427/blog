---
Published : true
---



## 1、cordova 打包 iOS (.ipa)     Android (.apk)

​                                                                                                        

##### 打包环境：   cordova 9.0.0    

#####                                                        ionic   4.1.2

#####                                  gradle 5.3.1

（此处环境版本为该教程编写版本，热更新版本也适用）



#### 使用cordova打包iOS Android app    



1、项目文件夹下，设置好代码内部需要部署的服务器(测试/正式)，命令行运行

```shell
$ npm run build
```

会生成一个dist文件夹，该文件夹下生成css、img、fonts、js文件夹和index.html文件。



2、新建cordova 项目，并添加iOS平台、 Android平台：

```shell
$ cordova create $(Name_of_app)
$ cordova platform add ios
$ cordova platform add android
```



3、把第一步生成的dist文件夹下的文件，拷贝到新建的空的cordova文件对应的www文件下,再配置项目.





4、 添加插件：为第二步建立的cordova项目添加必要的插件支持：

特别说明：当安装插件之后造成错误时，需要卸载对应的平台，再添加，才能有效。

``` shell
$ cordova plugin add cordova-plugin-splashscreen   //启动屏幕
$ cordova plugin add cordova-hot-code-push-plugin  //热更新需要
$ cordova plugin add cordova-plugin-statusbar      //状态栏显示
$ cordova plugin add cordova-plugin-camera
$ cordova plugin add https://github.com/giantss/cordova-plugin-ImagePicker.git


//以下是轨道交通项目完成文档时需要的插件支持：
cordova-plugin-camera 4.0.3 "Camera"
cordova-plugin-file 6.0.1 "File"
cordova-plugin-file-transfer 1.7.1 "File Transfer"
cordova-plugin-imagepicker 1.1.6 "ImagePicker"
cordova-plugin-splashscreen 5.0.2 "Splashscreen"
cordova-plugin-statusbar 2.4.2 "StatusBar"
cordova-plugin-whitelist 1.3.3 "Whitelist"



/**
*遇到的问题：build android 时 报错v4 ，
*解决办法详见：https://github.com/giantss/cordova-plugin-ImagePicker/issues/79：具体步骤：*在plugins/cordova-plugin-imagepicker/android/imagepicker.gradle文件中，在dependencies条*目下添加"implementation 'com.android.support:support-v4:+'"(双引号内的内容)，表示对低版本的
*支持。
*/
```



5、 配置图标和launch image: 在cordova 中的config.xml文件

App名称配置: coedova项目下的config.xml文件中，修改为：

```xml
<name>绍兴轨道交通</name>
```

配置启动屏幕(时间、消失形式)、状态栏(颜色，格式)、手机显示方向等： 添加到config.xml中

```xml
<preference name="Orientation" value="portrait" />
<preference name="WebViewBounce" value="false" />
<preference name="DisallowOverscroll" value="true" />
<preference name="StatusBarOverlaysWebView" value="false" />
<preference name="StatusBarStyle" value="default" />
<preference name="StatusBarDefaultScrollToTop" value="false" />
<preference name="ShowSplashScreenSpinner" value="false" />
<preference name="AutoHideSplashScreen" value="false" />
<preference name="SplashScreenDelay" value="10000" />
<preference name="FadeSplashScreen" value="false" />  
<preference name="StatusBarBackgroundColor" value="#ffffff" /> 
```



[配置config.xml的教程](<https://www.cnblogs.com/a418120186/p/5856371.html>)   以下为轨道交通项目v1.0.0发布时的图标及splash图片配置，配置启动图片和 icon内容放在 res文件夹内，形式见如下配置文件所示：

```xml
<platform name="android">
	<icon density="ldpi" src="res/icons/android/drawable-ldpi/ic_launcher.png" />
  <icon density="mdpi" src="res/icons/android/drawable-mdpi/ic_launcher.png" />
  <icon density="hdpi" src="res/icons/android/drawable-hdpi/ic_launcher.png" />
  <icon density="xhdpi" src="res/icons/android/drawable-xhdpi/ic_launcher.png" />
  <icon density="xxhdpi" src="res/icons/android/drawable-xxhdpi/ic_launcher.png" />
  <icon density="xxxhdpi" src="res/icons/android/drawable-xxxhdpi/ic_launcher.png" />
        
        <!-- 以下是欢迎页面，可根据需要进行添加 -->
  <splash density="land-hdpi" src="res/splashes/android/drawable-land-hdpi/screen.png" />
  <splash density="land-ldpi" src="res/splashes/android/drawable-land-ldpi/screen.png" />
  <splash density="land-mdpi" src="res/splashes/android/drawable-land-mdpi/screen.png" />
  <splash density="land-xhdpi" src="res/splashes/android/drawable-land-xhdpi/screen.png" />
  <splash density="land-xxhdpi" src="res/splashes/android/drawable-land-xxhdpi/screen.png" />
  <splash density="land-xxxhdpi" src="res/splashes/android/drawable-land-xxxhdpi/screen.png" />    
  <splash density="port-hdpi" src="res/splashes/android/drawable-port-hdpi/screen.png" />
  <splash density="port-ldpi" src="res/splashes/android/drawable-port-ldpi/screen.png" />
  <splash density="port-mdpi" src="res/splashes/android/drawable-port-mdpi/screen.png" />
  <splash density="port-xhdpi" src="res/splashes/android/drawable-port-xhdpi/screen.png" />
  <splash density="port-xxhdpi" src="res/splashes/android/drawable-port-xxhdpi/screen.png" />
  <splash density="port-xxxhdpi" src="res/splashes/android/drawable-port-xxxhdpi/screen.png" />    
</platform>
<platform name="ios">
        <!-- iOS 8.0+ -->
        <!-- iPhone 6 Plus  -->
        <icon src="res/icons/ios/icon-60@3x.png" width="180" height="180" />
        <!-- iOS 7.0+ -->
        <!-- iPhone / iPod Touch  -->
        <icon src="res/icons/ios/icon-20@3x.png" width="60" height="60" />
        <icon src="res/icons/ios/icon-60@2x.png" width="120" height="120" />
        <!-- iPad -->
        <icon src="res/icons/ios/icon-76.png" width="76" height="76" />
        <icon src="res/icons/ios/icon-76@2x.png" width="152" height="152" />
        <!-- iOS 6.1 -->
        <!-- Spotlight Icon -->
        <icon src="res/icons/ios/icon-40.png" width="40" height="40" />
        <icon src="res/icons/ios/icon-40@2x.png" width="80" height="80" />
        <!-- iPhone / iPod Touch -->
        <icon src="res/icons/ios/icon-57.png" width="57" height="57" />
        <icon src="res/icons/ios/icon-57@2x.png" width="114" height="114" />
        <!-- iPad -->
        <icon src="res/icons/ios/icon-20-ipad.png" width="20" height="20" />
        <icon src="res/icons/ios/icon-72.png" width="72" height="72" />
        <icon src="res/icons/ios/icon-72@2x.png" width="144" height="144" />
        <icon src="res/icons/ios/icon-83.5@2x.png" width="167" height="167" />
        <!-- iPhone Spotlight and Settings Icon -->
        <icon src="res/icons/ios/icon-29.png" width="29" height="29" />
        <icon src="res/icons/ios/icon-29@2x.png" width="58" height="58" />
        <icon src="res/icons/ios/icon-29@3x.png" width="87" height="87" />
        <!-- iPad Spotlight and Settings Icon -->
        <icon src="res/icons/ios/icon-50.png" width="50" height="50" />
        <icon src="res/icons/ios/icon-50@2x.png" width="100" height="100" />
        
        <icon src="res/icons/ios/icon-1024.png" width="1024" height="1024" />
        <!-- 以下是欢迎页面，可根据需要进行添加 -->
        <splash src="res/splashes/ios/Default~iphone.png" width="320" height="480"/>
        <splash src="res/splashes/ios/Default@2x~iphone.png" width="640" height="960"/>
        <splash src="res/splashes/ios/Default-Portrait~ipad.png" width="768" height="1024"/>
        <splash src="res/splashes/ios/Default-Portrait@2x~ipad.png" width="1536" height="2048"/>
        <splash src="res/splashes/ios/Default-Landscape~ipad.png" width="1024" height="768"/>
        <splash src="res/splashes/ios/Default-Landscape@2x~ipad.png" width="2048" height="1536"/>
        <splash src="res/splashes/ios/Default-568h@2x~iphone.png" width="640" height="1136"/>
        <splash src="res/splashes/ios/Default-667h.png" width="750" height="1334"/>
        <splash src="res/splashes/ios/Default-736h.png" width="1242" height="2208"/>
        <splash src="res/splashes/ios/Default-1792h.png" width="828" height="1792"/>
        <splash src="res/splashes/ios/Default-2436h.png" width="1125" height="2436"/>
        <splash src="res/splashes/ios/Default-2688h.png" width="1242" height="2688"/>
        <splash src="res/splashes/ios/Default-Landscape-736h.png" width="2208" height="1242"/>
        <splash src="res/splashes/ios/Default-Landscape-1792h.png" width="1792" height="828"/>
        <splash src="res/splashes/ios/Default-Landscape-2436h.png" width="2436" height="1125"/>
        <splash src="res/splashes/ios/Default-Landscape-2688h.png" width="2688" height="1242"/>
        
        <splash src="res/splashes/ios/Default-Landscape-No-StatusBar@2x~ipad.png" width="2048" height="1496"/>
        <splash src="res/splashes/ios/Default-Landscape-No-StatusBar~ipad.png" width="1024" height="748"/>
        <splash src="res/splashes/ios/Default-No-StatusBar@2x~ipad.png" width="1536" height="2008"/>
        <splash src="res/splashes/ios/Default-No-StatusBar~ipad.png" width="768" height="1004"/>
        

```



6、配置完xml文件之后，需要执行如下命令进行重新build项目：

```shell
$ cordova platform rm ios
$ cordova platform add ios
```

同样，android也需要相同的操作：

```shell
$ cordova platform rm android
$ cordova platform add android
```

7、到此，所有公共配置已经完成，若进行调试程序，可以直接运行：

```shell
运行ios模拟程序：
$ cordova run ios 

运行安卓模拟程序
$coedova run android
```

下面将分别进行iOS-ipa、安卓-apk的打包、签名、发布设置；



> ## 1、iOS签名与打包发布 

我们使用Xcode 进行打包，然后使用Xcode 自带的工具Application Loader进行ipa的上传App store商店：

准备阶段：进入apple 开发者网站，进入证书管理中，建立发布签名证书——> App IDs ———>Provision Profile文件

签名证书的制作需要本地使用秘钥引导工具,从证书颁发机构请求证书，选择存到磁盘选项，生成CertificateSigningRequest.certSigningRequest文件，上传该请求证书才能生成发布证书。然后根据发布证书在开发者网站上生成App IDs  最后生成描述文件。

1、打开使用xcode 打开platforms/ios/绍兴轨道交通.xcworkspace (显示为白色文件图标的文件)。

2、打开后需要进行打包前的配置：需要provision profile描述文件  

​								signing Certification签名证书

​	2.1、填写描述文件必须的bundle identifier ,一般为com.ecidi.scdtpm这种格式，即com.公司缩写.项目名

​	若你具有付费的Apple ID账号，可以登录，并进行自动签名设置；若没有账号的使用权，也可以使用该账号所有人提供的描述文件、签名证书和个人开发证书，使用该账号进行手动的配置。

​	2.2、打开项目的Edit scheme,将左侧各项Run、Build、Test、Profile、Archive设置成release模式。

​	且，Run下的Diagnostics选项下，取消选择Address  Sanitizer 和 Zombie Objects (如果选中的话就取消选中)。

​	2.3、将模拟器选择模块选择Generic iOS Device选项

​	2.4、检查需要部署的最低iOS版本，默认为10.0，可以选择9.0，选择Target — build settings 然后搜索code sign ,在显示的条目中，若使用自动签名，需要将code signing Identity 全部设置为 iOS Developer ;若手动签名，则都需要设置为你使用发布账号的开发者发布签名证书，(形如iPhone Distribution:xxxxx).



3、选择菜单栏Product下的Archive 进行归档操作，等build完成后进入Archive information界面。



4、此时需要进入开发者账号的itunes connection中创建自己的App,填写项目，信息等，细节包含隐私网址，宣传文本，副标题，App名称，icon图标，屏幕快照(可以在虚拟机中进行对应不同机型的快照截取)，填写完整信息，就可以保存提交审核。



5、此时，返回第3步的界面，点击Validate App 对打包前的设置进行检查，无错误就会显示successful 后面会有绿色的✅。

6、再点击Distribute App 选择导出包，生成带有日期字符名称的文件夹，文件夹中包含xxxx.ipa文件和其他文件。

7、打开Xcode 菜单栏  Xcode/open Develop Tool/Application Loader 打开，登录，这里需要一个特殊密码(账号开启二次认证的情况下)，只需点击页面上的蓝色链接，进入apple 登录页面，登陆进去，点击特殊密码，然后输入账号密码，会弹出显示的密码窗，复制，粘贴到Application Loader中来就可以登录。



8、选择生成的xxxx.ipa文件，这里需要提前将xxx.ipa的名称改为全英文的，不然会报错，因为ipa包名称不允许为中文。

9、等待完成，显示成功、等待审核和感谢界面。



> ## 2、安卓签名打包设置：

1、首先，运行：

```shell
$ cordova build --release android 
```

进行未签名包的打包操作：app-release-unsigned.apk 位于platform/android/app/build/outputs/apk/release文件夹下，备用。



2、生成JKS证书：

```shell
$ keytool -genkeypair -alias sxdtpm -keyalg RSA -validity 36500 -keystore sxdtpm.keystore
```

记住填写的密码，其他的根据实际填写，最后是否正确？要填写：是。最后生成文件的sxdtpm.keystore就是我们需要的签名文件。



3、将第一步生成的未签名文件app-release-unsigned.apk 和签名证书sxdtpm.keystore 放在一个文件夹中(便于命令中地址的书写,也可以不这么做，但是命令行的语句就会显得不美观），在当前目录下，执行：

```shell
/**
*jarsigner -verbose -keystore [您的私钥存放路径] -signedjar [签名后文件存放路径] [未签名的文件路径] *[您的证书的别名] 
*/
例：
$ jarsigner -verbose -keystore sxdtpm-release.keystore -signedjar sxdtpm-official-release.apk app-release-unsigned.apk sxdtpm
```

最后生成的sxdtpm-official-release.apk文件就是签完名的安卓打包文件。



## 2、cordova热更新app

cordova 9.0.0 版本已经不支持cordova-hot-code-push-plugin插件，

所以使用热更新，必须使用较低cordova版本。

cordova 8.0.0

Ionic 4.12.0

Gradle 4.4



添加平台时候，使用如下命令：默认cordova 8.0.0 添加的ios版本为4.5  androd版本为7.0

```shell
$ cordova platform add ios@~5.0.0
$ cordova platform add android@~8.0.0
```

该命令 指定添加ios5.0.0版本，android8.0.0版本



1、添加插件：

```shell
$ cordova plugin add cordova-hot-code-push-plugin

```



2、添加代码热更新客户端：

```shell
$ npm install -g cordova-hot-code-push-cli
```



3、初始化：在cordova打包项目根目录下执行：

```shell
$ cordova-hcp init
```

随后进行一些字段的填写，其中

> name:随意写；

> 有关amazon的直接回车跳过不填写；

> ios_identifier可以写iOS上线app中的appIDs号；

> android_identifier暂时不上线安卓商城，可以不写。

> update可以填写

> > ​       now：启动下载更新后就进行更新；

> > ​       start:应用启动再更新。一般情况是，有更新时，用户重新(需完全退出)进入app后，下载更新的内 容，下次再重新启动进入app时进行更新操作。

> > ​      resume:有更新后第一次完全退出后进入app进行下载，当app从后台回复时候进行更新操作。

> content_url表示热更新的服务器地址和端口号（见步骤6），写到chcp.json文件的上一级文件夹，如http://10.210.19.215:8080/www/



完成后，在cordova项目的根目录下，生成cordova-hcp.json文件，进入文件，添加字段：

```vue
"min_native_interface": 1
```

表示app外壳最小支持版本为1。该字段与app升级有关，若只关心热更新，该字段可忽略。





4、配置cordova项目的config.xml文件：

```xml
 <chcp>
        <auto-download enabled="true" />
        <auto-install enabled="true" />
        <native-interface version="1" />
        <config-file url="http://10.214.39.211:10086/sxdt/chcp.json" />
    </chcp>
```

其中config-file url 的配置必须是热更新服务器的地址下的http可访问的chcp.json文件。

native-interface表示当前的app外壳版本号，该字段是做app升级提示的依据。

auto-download置为true表示自动下载。

auto-install置为true表示自动安装 



5、生成/更新www文件夹内的版本信息文件和MD5校验文件，即chcp.json和chcp.manifest

```shell
$ cordova-hcp build
```

生成上面所述两个文件，

**以后每次热更新，只需要将修改后build之后的dist文件夹的文件，拷贝到cordova打包项目的www文件夹下，再进行该步骤的操作，将生成的www下的文件放到热更新服务器上对应的文件夹下即可。**



6、建立临时http可访问服务器：

```shell
$ npm install -g serve
```

执行完之后出现矩形框，内部有本地和http访问的地址。该窗口关闭，代表服务器关闭，不要关闭该终端或跳出执行其他命令。



在需要使用的文件夹内，另起终端，执行：

```shell
$ serve -p 8080
```

表示当前路径http  8080端口可访问，可以在该目录下创建文件夹与文件，http通过地址通过指定端口可以访问下面的文件和文件夹。



7、在vue项目中，修改App.vue文件：添加hotPush方法链：

```javascript
onDeviceReady() {  
//在app的生命周期方法中，添加hotPush()方法调用，下面表示设备完成加载后执行热更新的push操作
         this.hotPush() //热更新
        document.addEventListener("backbutton", this.eventBackButton, false); 
        console.log(StatusBar)
        navigator.splashscreen.hide();
      },
      //返回键点击响应
      eventBackButton() {
        if (this.$route.name == "login") {
          document.addEventListener("backbutton", this.exitApp, false);   
        } else if (this.$route.meta.toast) {
          this.$vux.toast.show({
            type: "text",
            text: '再点一次退出!',
            position: 'bottom'
          })
          document.removeEventListener("backbutton", this.eventBackButton, false); 
          document.addEventListener("backbutton", this.exitApp, false);   
          var intervalID = setInterval(
            () => {
              clearInterval(intervalID);
              document.removeEventListener("backbutton", this.exitApp, false);   
              document.addEventListener("backbutton", this.eventBackButton, false); 
            },
            3000
          );
        } else {
          this.$router.go(-1);
        }
      },
      exitApp() {
        navigator.app.exitApp();
      },
      hotPush() { //热更新主方法 
		//使用chcp热更新插件，检查可更新的内容，如有就执行
        chcp.installUpdate(this.installationCallback);
        chcp.configure({
            "config-file": "http://10.214.39.211:10086/sxdt/chcp.json" // 配置热更新服务端
          },
          this.configureCallback); //检查版本调用
      },
	//通过热更新服务器检查，时间戳和app外壳版本信息，决定进行下载还是提示app更新
      configureCallback(error) {
        if (error) {
          console.log('Error during the configuration process');
          console.log(error);
        } else {
          console.log('Plugin configured successfully');
          this.checkForUpdate(); //调用app升级提示方法
        }
      },

      checkForUpdate() {
		//获取服务器端的数据信息，包括版本信息，若版本无变动，则下载热更新内容，版本有变动则执行回调方法
        chcp.fetchUpdate(this.fetchUpdateCallback);
      },
		
	//获取服务器数据的回调方法
      fetchUpdateCallback(error, data) {
        let _this = this
        if (error) {
          console.log('Failed to load the update with error code: ' + error.code);
          console.log(error.description);
          if (error && error.code == chcp.error.APPLICATION_BUILD_VERSION_TOO_LOW) {
            this.$vux.confirm.show({ //提示更新app版本，提示框
              // 组件除show外的属性
              title: "提示",
              content: "您的app版本过低，请升级",
              onCancel() {
                _this.exitApp()
              },
              onConfirm() {//用户点击确认执行的回调
                _this.userWentToStoreCallback()
              }
            })
          }
        }
        console.log(data);
      },

      installationCallback(error) {
        if (error) {
          console.log('Failed to install the update with error code: ' + error.code);
          console.log(error.description);
          this.onUpdated()
        } else {
          console.log('Update installed!');
          this.onUpdated()
        }
      },
      onUpdated() {
        navigator.splashscreen.hide();
      },
      userWentToStoreCallback() { //用户点击回调方法
        
      cordova.InAppBrowser.open('https://xxxxxxxx/xxxxxxx', '_system', '') //手机浏览器跳转地址    
                     //苹果商店轨道交通apphttps://itunes.apple.com/cn/app/id1459832528?mt=8 
        this.exitApp()
      },
    },
```



8、完成所有配置，执行打包的操作，将生成的dist文件夹下的文件拷贝到cordova项目中的www文件夹下，

执行第5部。



（App升级提示部署设置：根据是否更新cordova 插件的情况来评估 是否需要升级外壳App，若升级外壳，则需要修改config.xml文件内的native-interface的本地版本，然后修改cordova-hcp.json内部的mini-native-interface版本号，再执行第5步，外壳升级必须保证iOS端升级版本可下载，apk升级版本已放到扫二维码下载的服务器上。）

***

至此，所有cordova打包和热更新的内容就结束了。有问题邮件联系。

