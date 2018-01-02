# 制作开源库到CocoaPods

### 第一步：在GitHub创建仓库（repository）
![](./p1.png)

### 第二步：克隆(clone)到本地

`git clone git@github.com:starlordss/SKit.git`

或者

`git clone https://github.com/starlordss/SKit.git`

![](./p2.png)

### 第三步：创建podsepc文件
* 进入项目文件目录中：`cd SKit`
![](./p12.png)

* `pod spec create SKit git@github.com:starlordss/SKit.git` 

> 注意:这里使用SSH不要使用URL，否则会报错

> `SocketError - Failed to open TCP connection to api.github.com:443 (getaddrinfo: nodename nor servname provided, or not known)`

* 或者 `pod spec create SKit`

> `pod spec create`命令会在你当前目录下生成podsepc文件，该文件是描述pod相关的信息的



### 第四步：配置podsepc文件
* 你可以用Xcode直接打开xxx.podsepc文件
![](./p10.png)
* 修改podsepc配置文件

```ruby
Pod::Spec.new do |s|
  s.name             = 'SKit'
  s.version          = '0.0.1'
  s.summary          = 'This is a kit for iOS'
  s.description      = <<-DESC
TODO: Add long description of the pod here.Add long description of the pod here.
                       DESC

  s.homepage         = 'https://github.com/starlordss/SKit'
  s.license          = { :type => 'MIT', :file => 'LICENSE' }
  s.author           = { '星眔' => 'isstarz@163.com' }
  s.source           = { :git => 'https://github.com/starlordss/SKit.git', :tag => s.version.to_s }

  s.ios.deployment_target = '8.0'
  s.source_files = 'SKit/Classes/**/*'
  s.requires_arc = true
end
```

> 源码文件路径：

> `/**`表示该目录下所有文件；
> `*.{h,m}`表示匹配所有以.h和.m为扩展名的文件

### 第五步: 将podsepc文件推送到GitHub并打tag
* `git add -A && git commit -m "创建版本 0.0.1."`
* `git tag '0.0.1'`
* `git push origin master --tags`

### 第六步: 验证.podspec文件
* `pod spec lint`
![](./p7.png)


### 第七步: 注册CocoaPods
* 注册CocoaPods 需要你登录邮箱点击链接验证

`pod trunk register xxx@email.com 'SKit'`

* 点击邮箱链接验证通过，验证是否正常<会有延迟>

`pod trunk me`
![](./p11.png)


第八步: 将.podspec文件推送到CocoaPods/repo

`pod trunk push xxx.podspec`


> [!] Failed to connect to GitHub to update the CocoaPods/Specs specs repo - Please check if you are offline, or that GitHub is down
> 出现上面的报错，是服务器问题，需要等个几分钟重复上面的命令





