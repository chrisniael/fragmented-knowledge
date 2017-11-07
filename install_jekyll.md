# 安装 Jekyll

## 安装最新版的 Ruby

```bash

yum install epel-release

yum install readline-devel zlib-devel libffi-devel libyaml-devel openssl-devel sqlite-devel

gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB

curl -sSL https://get.rvm.io | bash -s stable

source /etc/profile.d/rvm.sh
rvm reload

rvm requirements run

rvm list known

rvm install 2.4
	
rvm use 2.4 --default
```

## Gem 安装 Jekyll

```bash
gem install jekyll jekyll-paginate jekyll-assets kramdown
```

## 参考

[RVM](https://rvm.io/)
[Install Ruby 2.4 (theshell.guru)](https://www.theshell.guru/install-ruby-2-4-centos-7-3/)
