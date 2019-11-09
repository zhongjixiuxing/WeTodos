# WeTodos

 Alike [microsoft todos](https://to-do.microsoft.com/) application

[微信小程序客户端体验程序](https://github.com/zhongjixiuxing/WeTodos-miniprogram)：

<img align="left" width="150" height="150" src="https://ae01.alicdn.com/kf/Ha2cefce2dde94730ab017ceb910f5e99H.jpg" />
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>




## Setup(local)
**本地环境不需要AWS、Serverless、正式环境的小程序账号和备案域名**	



 * 采用git clone 项目代码到本地

   ```bash
   git clone https://github.com/zhongjixiuxing/WeTodos --recurse-submodules
   ```

 * 启动本地serverless 服务. 默认为**3000**端口

   ```bash
   cd serverless && npm i && npm run start
   ```

 * 打开Wechat 官方的[小程序开发工具](https://developers.weixin.qq.com/miniprogram/dev/devtools/download.html), 导入miniprogram 目录的项目到小程序开发工具中，即可看到小程序页面。

   > Tips: 
   > * 注意这里需要更改 **miniprogram/config.js** 配置文件里面的**apollo** 访问URL为localhost:3000.
   > * 如果没有小程序账号，可以申请用[小程序的测试账号](https://developers.weixin.qq.com/miniprogram/dev/devtools/sandbox.html)
   



## Deploy on AWS
**Require, before you do**
 * AWS Cloud 的激活账号
 * 注册一个 Serverless.com 账号
 * Wechat 小程序账号
 * 中国大陆内已备案的域名一个(小程序服务硬性要备案的域名)



1. ***Deploy Serverless service***

   *  在[serverless dashboard](https://dashboard.serverless.com/tenants/anxing/applications/) 中新建一个APP，命名为wetodos (当然，你也可随你喜欢命名，到时需要更改serverless.prod.yaml 文件里面的app 字段即可)

   * 在命令行下安装serverless tool

     ```bash
     npm install serverless --global
     ```

   * 登陆serverless 账号在命令行终端下

     ```bash
     serverless login
     ```

     这将会打开默认的浏览器，默认授权下去即可。

     授权后回到命令行终端下，你将会见到授权成功的英文输出信息

   * 进入到serverless profiles 下的default 配置文件页面

     ![image-20191101100525040](https://ae01.alicdn.com/kf/H8c27d63aa2a740d595f547ed3cad71ebt.png) 

   * 授权serverless AWS IAM

     ​		![image-20191101100724192](https://ae01.alicdn.com/kf/H96c3e85cda1c4a0488393d44e9fa0dd1U.png)

   * 进入到AWS 授权页面，所有操作都是点击下一步即可。

   * 授权回来后点击Paramters 配置一些部署参数

     * ![image-20191101101054832](https://ae01.alicdn.com/kf/Hded66639220a46ceb97c68aee5828491t.png)

   * ![image-20191101101207909](https://ae01.alicdn.com/kf/H9422f79f7f984e118d8c539df0a39f14G.png)

     一共有四个参数需要配置的

     **wxAppId**:  wechat 小程序的appid
     **wxAppSecret**:  wechat 小程序的secret
     **jwtPubKey**:  项目的RSA 的公开证书的Base64 编码。

​						RSA 自行google/百度 search **RSA 证书生成**关键字操作
​     
​     ​						注意这里是将public 证书的内容通过base64 编码后的内容哦，
​     
​     ​						public证书的内容首尾不能有空格和换行符
​     **jwtPriKey**:  项目的RSA 的私有证书的Base64 编码。同上


​     
​     
   *  然后保存退出，在命令行终端下执行
   
      ```bash
      cd serverless && npm run deploy:prod
      ```
   
      稍等几分钟后自动部署完后，看到下面的输出，endpoints 就是aws lambda 访问地址
   
      ![image-20191101103054685](https://ae01.alicdn.com/kf/H68acff7dd8a3454ebe45f5884e410cfeM.png)
   
   * 根据上面的AWS Lambda 访问地址替换 miniprogram/config.js 里面apollo的访问地址即可

<br />      
      

## Issues

 * [Git Submodule](https://blog.devtang.com/2013/05/08/git-submodule-issues/)

