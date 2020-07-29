# CosUploader #

上传到腾讯云 COS 对象云存储上传控件(仿*百度webuploader*)

# 使用说明 #

### 1. 首先在 COS 控制台中，开好跨域，(见预览图文件夹中跨域图片)详情见 https://console.cloud.tencent.com/cos5/bucket
### 2. 本工程需要启动服务，不能直接file://这样子访问！！！！
### 3. 找后台要获取配置信息的接口，
   ```
   var applyTokenDo = function () {
     var client = new COS({
       getAuthorization: function (options, callback) {
         // 异步获取临时密钥
         $.get('http://example.com/server/sts.php', {
             bucket: options.Bucket,
             region: options.Region,
         }, function (data) {
             var credentials = data && data.credentials;
             if (!data || !credentials) return console.error('credentials invalid');
             callback({
                 TmpSecretId: credentials.tmpSecretId,
                 TmpSecretKey: credentials.tmpSecretKey,
                 XCosSecurityToken: credentials.sessionToken,
                 // 建议返回服务器时间作为签名的开始时间，避免用户浏览器本地时间偏差过大导致签名错误
                 StartTime: data.startTime, // 时间戳，单位秒，如：1580000000
                 ExpiredTime: data.expiredTime, // 时间戳，单位秒，如：1580000900
             });
         });
       }
     });
     return client;
   };
   ```
   若暂无后台，前端自己调测上传功能，则见4，
### 4. 在代码中配置好 bucket、region、accessKeyId、accessKeySecret。(仅限前端自己做测试)，
### 然后就可以上传啦！！


# 功能 #
- [x] 上传多个文件
- [x] 继续添加功能
- [x] 图片预览


### 百度 webuploader ### 
https://github.com/fex-team/webuploader

#### 腾讯云 COS ###
https://cloud.tencent.com/product/cos

#### 腾讯云 COS JS SDK ###
https://github.com/tencentyun/cos-js-sdk-v5

