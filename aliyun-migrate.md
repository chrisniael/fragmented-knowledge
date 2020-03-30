# 阿里云迁移记录

## 停用安全加固

购买的时候，在 **镜像** 选项那边别勾选 **安全加固**。

## 停用 aliyun-service

```bash
systemctl status aliyun.service
systemctl stop aliyun.service
systemctl disable aliyun.service
```

## 一些软件

```bash
yum install -y htop git
```

不要安装 epel-release，阿里云的 CentOS 8 系统默认配置了 epel 的 yum 源了。

## Nginx

```bash
yum install -y nginx
systemctl status nginx
systemctl start nginx
systemctl enable nginx
```


## Let's Encrypt

https://certbot.eff.org/

## jekyll

#### Ruby 开发环境

```bash
yum install -y ruby gcc gcc-c++ make
```


### uninitialized constant Gem::RDoc

```bash
gem install -V rdoc
```

#### 安装 jekyll 和 bundler

```bash
gem install -V jekyll bundler
```

###### jekyll, mkmf.rb can't find header files for ruby at /usr/share/include/ruby.h

```bash
yum install -y ruby-devel
```

###### jekyll, gcc: error: /usr/lib/rpm/redhat/redhat-hardened-cc1: No such file or directory

```bash
yum install -y redhat-rpm-config
```

###### nokogiri, zlib is missing; necessary for building libxml2

```bash
yum install -y zlib-devel
```

###### jekyll-assets, tar

```bash
yum install -y tar
```


## nodejs

```bash
yum install nodejs npm
```

#### pm2
```bash
npm install -g pm2

# pm2 start ...
pm2 save
pm2 startup
```
