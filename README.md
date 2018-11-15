# Laravel-SendCloud
Laravel 5.X 的 SendCloud 驱动

##### 优点：
普通发送方式完全兼容官方用法，可随时修改配置文件改为其他驱动，而不需要改动业务代码

## 安装

在项目目录下执行

```
composer require jackwiy/sendcloud
```

## 配置

修改 `config/app.php`，添加服务提供者

```php
'providers' => [
   // 添加这行
    JackWiy\Mail\SendCloudServiceProvider::class,
];
```

在 `.env` 中配置你的密钥， 并修改邮件驱动为 `sendcloud`

```ini
MAIL_DRIVER=sendcloud

SEND_CLOUD_USER=     # 创建的 api_user
SEND_CLOUD_KEY=      # 分配的 api_key
SEND_CLOUD_TIMEOUT=  # 请求超时 api_timeout
```

## 使用

#### 普通发送：
用法完全和系统自带的一样, 具体请参照官方文档： https://laravelacademy.org/post/8977.html

```php
Mail::send('emails.welcome', $data, function ($message) {
    $message->from('us@example.com', 'Laravel');

    $message->to('foo@example.com')->cc('bar@example.com');
});
```

#### 模板发送
用法和普通发送类似，不过需要将 `body` 设置为 `SendCloudTemplate` 对象

> 使用模板发送不与其他邮件驱动兼容 ！！！

```php
// 模板变量
$bind_data = ['url' => 'http://jackwiy.me'];
$template = new SendCloudTemplate('模板名', $bind_data);

Mail::raw($template, function ($message) {
    $message->from('us@example.com', 'Laravel');

    $message->to('foo@example.com')->cc('bar@example.com');
});
```
