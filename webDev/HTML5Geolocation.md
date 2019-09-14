# HTML5定位的使用，及定位失败的原因
> HTML5 Geolocation API 用于获取用户定位。该规范提供了一套保护用户隐私的机制。必须先得到用户明确许可，才能获取用户的位置信息。
## 定位(Geolocation)的使用
**获取当前地理位置：**
`navigator.geolocation.getCurrentPosition(successCallback, errorCallback, options)`
**获取定位变化后当前地理位置：**
`navigator.geolocation.watchPosition(successCallback, errorCallback, options)`
#### 参数
 **successCallback**
&emsp;&emsp;成功得到位置信息时的回调函数，使用`Position`对象作为唯一的参数。
**errorCallback** *[可选]*
&emsp;&emsp;获取位置信息失败时的回调函数，使用 `PositionError` 对象作为唯一的参数，这是一个可选项。
**options** *[可选]*
&emsp;&emsp;一个可选的`PositionOptions`对象。

`Geolocation.watchPosition()` 用于注册监听器，在设备的地理位置发生改变的时候自动被调用。也可以选择特定的错误处理函数。
该方法会返回一个 ID，如要取消监听可以通过  `Geolocation.clearWatch()` 传入该 ID 实现取消的目的。
```javascript
id = navigator.geolocation.watchPosition(success[, error[, options]])
```
#### 实例
````js
var options = {
  enableHighAccuracy: true,
  timeout: 5000,
  maximumAge: 0
};

function success(pos) {
  var crd = pos.coords;

  console.log('Your current position is:');
  console.log('Latitude : ' + crd.latitude);
  console.log('Longitude: ' + crd.longitude);
  console.log('More or less ' + crd.accuracy + ' meters.');
};

function error(err) {
  console.warn('ERROR(' + err.code + '): ' + err.message);
};

navigator.geolocation.getCurrentPosition(success, error, options);
````

## 定位出现失败的原因
#### 1. 第一种情况
浏览器不支持原生定位接口，如IE较低版本的浏览器，message字段包含`Browser not Support html5 geolocation`信息。
#### 2. 第二种情况
用户禁用了定位权限，需要用户开启定位权限，message字段包含`Geolocation permission denied`。
#### 3. 第三种情况
浏览器禁止了非安全域的定位请求，比如Chrome、IOS10已经陆续禁止，需要升级站点到HTTPS，message字段包含`Geolocation permission denied`信息。**注意:**Chrome不会禁止`localhost`域名HTTP协议下的定位。
#### 4. 第四种情况
浏览器定位超时，包括原生的超时，可以适当增加超时属性的设定值以减少这一现象。某个别浏览器本身对定位接口的友好程度较弱，也会超时返回失败，message字段包含`Geolocation time out`信息。
#### 5. 第五种情况
Chrome、Firefox以及一些套壳浏览器接入的定位服务在国外，有较大的限制，也会造成定位失败，且失败率较高。