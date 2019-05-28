

# 一、Java

## 1、事务回滚

``` java
TransactionAspectSupport.currentTransactionStatus().setRollbackOnly();
```

## 2、时间过期

```java
LocalDateTime time = LocalDateTime.parse(taskRegEntity.getEndDate() + taskRegEntity.getEndTime(),

        DateTimeFormatter.ofPattern(DateUtil.YYYYMMDDHHMMSS))

        .plusMinutes(sysParamService.getPhoneRegisterParamExpire());

if (LocalDateTime.now().isAfter(time)) {

    return R.error("验证码已过期");

}
```

## 3、随机生成字符串

```java
Base64Utils.encodeToString(UUID.randomUUID().toString().getBytes(StandardCharsets.UTF_8));
```

## 4、Optional 

Optional.of()或者Optional.ofNullable()：创建Optional对象，差别在于of不允许参数是null，而ofNullable则无限制。

## 5、MD5加密

```java
public class Md5Uitls {
    private static String byteArrayToHexString(byte b[]) {
        StringBuffer resultSb = new StringBuffer();
        for (int i = 0; i < b.length; i++)
            resultSb.append(byteToHexString(b[i]));

        return resultSb.toString();
    }

    private static String byteToHexString(byte b) {
        int n = b;
        if (n < 0)
            n += 256;
        int d1 = n / 16;
        int d2 = n % 16;
        return hexDigits[d1] + hexDigits[d2];
    }

    public static String MD5Encode(String origin, String charsetname) {
        String resultString = null;
        try {
            resultString = new String(origin);
            MessageDigest md = MessageDigest.getInstance("MD5");
            if (charsetname == null || "".equals(charsetname))
                resultString = byteArrayToHexString(md.digest(resultString
                        .getBytes()));
            else
                resultString = byteArrayToHexString(md.digest(resultString
                        .getBytes(charsetname)));
        } catch (Exception exception) {
        }
        return resultString;
    }

    private static final String hexDigits[] = { "0", "1", "2", "3", "4", "5",
            "6", "7", "8", "9", "a", "b", "c", "d", "e", "f" };
}
```

## 6、注解切面（Aspect）

新建Login注解

```java
/**
 * 登录效验
 * @author chenshun
 * @email sunlightcs@gmail.com
 * @date 2017/9/23 14:30
 */
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
@Documented
public @interface Login {
}
```

配置Aspect切面注解

```java
@Aspect
@Component
public class LoginAspect {
    @Pointcut("@annotation(com.annotation.Login)")
    public void loginCut() {

    }
    @Before("loginCut()")
    public void dataFilter(JoinPoint point) throws Throwable {
        Object params = point.getArgs();
        System.out.println(params);
        return;
    }
}
```

使用切面注解

```java
@Login
@RequestMapping("hello")
@ResponseBody
public String test(){
    return "asp测试";
}
```

# 二、 JS

## 1、手机正则表达式

```javascript
isBlank(vm.info.managerTel) || !/^((1[3,5,8][0-9])|(14[5,7])|(17[0,6,7,8])|(19[7]))\d{8}$/.test(vm.info.managerTel)
```

## 2、金额正则表达式

```
var reg = /^(([1-9]\d{0,5})|(0))(\.\d{0,2})?$/;
```

## 

## 3、Js获取input type=“file”里的的file （或Blod）转换base64

```js
<input type="file" name="" onchange="getFile(this)" value="upload"/>
    
function getFile(obj){
    console.log()
    var blodFile = obj.files[0];
    console.log(blodFile);
    var reader = new FileReader();
    reader.readAsDataURL(blodFile);
    reader.onload = function(){
        $("#picture").attr("src",reader.result);
    }
}

```

## 4、Base64转换成Blod

```js
convertBase64ToBlob: function(base64){
    var base64Arr = base64.split(',');
    var imgtype = '';
    var base64String = '';
    if(base64Arr.length > 1){
        //如果是图片base64，去掉头信息
        base64String = base64Arr[1];
        imgtype = base64Arr[0].substring(base64Arr[0].indexOf(':')+1,base64Arr[0].indexOf(';'));
    }
    // 将base64解码
    var bytes = atob(base64String);
    //var bytes = base64;
    var bytesCode = new ArrayBuffer(bytes.length);
    // 转换为类型化数组
    var byteArray = new Uint8Array(bytesCode);
    // 将base64转换为ascii码
    for (var i = 0; i < bytes.length; i++) {
        byteArray[i] = bytes.charCodeAt(i);
    }
    // 生成Blob对象（文件对象）
    return new Blob( [bytesCode] , {type : imgtype});
}
```

## 5、保留两位小数

```js
Math.floor(acctData * 100) / 100 ;
```

## 6、JavaScript concat()

concat() 方法用于连接两个或多个数组。

该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。

## 7、splice()的用法

* 删除功能，第一个参数为第一项位置，第二个参数为要删除几个。

* 插入功能，第一个参数（插入位置），第二个参数（0），第三个参数（插入的项）

  array.splice(index,0,insertValue)，返回值为空数组，array值为最终结果值

* 替换功能，第一个参数（起始位置），第二个参数（删除的项数），第三个参数（插入任意数量的项）

  array.splice(index,num,insertValue)，返回值为删除内容，array为结果值。

## 8、arrayObject.reverse()  颠倒顺序

##  9、获取浏览器地址的参数

```js
/**
 * 获取浏览器地址的参数
 */
function getParam(key) {
    var href = location.href;
    var index = href.indexOf('?');
    if(index > 0) {
        var parArr = href.substring(index + 1).split('&');
        for(var i in parArr) {
            var kvArr = parArr[i].split('=');
            if(kvArr[0] == key) {
                return kvArr[1];
            }
        }
    }
    return '';
}
```

# 三 Git

## 1、本地项目pull到gitHub

![1558583426090](C:\Users\Administration\AppData\Roaming\Typora\typora-user-images\1558583426090.png)







# 四、Linxu

## 1、rz 不能用

~~~linxu
sudo yum install -y lrzsz //sudo可无
~~~

## 2、 删除文件

~~~ linux
rm -f 文件名
~~~

## 3、解压 

~~~linux
tar -zxvf 文件名
~~~

## 4、安装JDK

查看是否存在jdk

~~~linux
java -version
~~~

## 5、防火墙

2019-05-28T02:14:01.788139Z 5 [Note] [MY-010454] [Server] A temporary password is generated for root@localhost: cBWv1MpMe:Vy

~~~linux
firewall-cmd --zone=public --list-ports 防火墙列表
systemctl status firewalld查看firewalld状态
systemctl start firewalld开启防火墙
systemctl stop firewalld 关闭防火墙设置
systemctl enable firewalld.service  #设置开机启用防火墙
systemctl disable firewalld.servic  #设置开机不启动防火墙
firewall-cmd --reload 刷新
~~~

### A、添加开放端口

1、firewall-cmd --permanent --add-port=80/tcp    #–permanent 每次启动防火墙加载此规则

2、firewall-cmd --reload

### B、关闭端口

firewall-cmd --permanent --remove-port=80/tcp     #–permanent 每次启动防火墙加载此规则

## 6、网卡

~~~linux
ifup lo 启用lo网卡
~~~

## 7、查看端口状态

~~~linux
netstat -an | grep 8080
~~~

## 8、搜索查看进程

~~~linux
ps -ef |grep tomcat
~~~

## 9、杀死进程

~~~linux
kill -9 进程名称
~~~

## 10、安装telnet应用

```
	telnet 127.0.0.1 80
	yum list telnet*              列出telnet相关的安装包
    yum install telnet-server          安装telnet服务
    yum install telnet.*           安装telnet客户端
```

# 五、**Tomcat**

## 1、启动时卡在[localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory

将java目录的$JAVA_HOME/jre/lib/security/java.security内的securerandom.source参数修改为file:/dev/./urandom

## 2、启动关闭

~~~linux
/usr/tomcat/apache-tomcat-8.5.41/bin/startup.sh
/usr/tomcat/apache-tomcat-8.5.41/bin/shutdown.sh
~~~

## 3、查看启动日志

tail  -f  /usr/tomcat/apache-tomcat-8.5.41/logs/catalina.out  日志