## yii2配置发送邮件



##### 配置：common/config/main.php 在components下面添加：

```php
'mailer' => [
     'class' => 'yii\swiftmailer\Mailer',
     'useFileTransport' =>false,//这句一定有，false发送邮件，true只是生成邮件在runtime文件夹下，不发邮件
     'transport' => [
         'class' => 'Swift_SmtpTransport',
         'host' => 'smtp.qq.com',  //每种邮箱的host配置不一样
         'username' => '',
         'password' => '',//如果是QQ邮箱需要开启smtp服务，发送验证码后出现授权码。
         'port' => '465',
         'encryption' => 'ssl',
     ],
     'messageConfig'=>[
         'charset'=>'UTF-8',
         'from'=>['******@QQ.com'=>'name']//设置发送人名称，在微信的QQ邮箱中和QQ客户端的邮箱上显示，但是在QQ邮箱APP中还是显示******@QQ.com
     ],
],
```





##### controller：

```php
$mail= Yii::$app->mailer->compose();
            $mail->setTo('收件人邮箱');
            $mail->setSubject("标题");
            $mail->setHtmlBody("<br>内容");//可以添加HTML标签
            if($mail->send())
            {
                echo 'success';
            }
```

