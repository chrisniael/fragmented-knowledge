# CentOS 7 安装 Jekyll

## 卸载 Yum 安装的 Ruby

```bash
for x in `gem list --no-versions`; do gem uninstall $x -a -x -I; done
yum remove ruby
```

## 安装 RVM

```bash
yum groupinstall "Development Tools"
yum install epel-release
yum install readline-devel zlib-devel libffi-devel libyaml-devel openssl-devel sqlite-devel
```

```bash
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
curl -sSL https://get.rvm.io | bash -s stable
```

```bash
source /etc/profile.d/rvm.sh
rvm reload
```

```bash
rvm requirements run
```

## RVM 安装 Ruby

```bash
rvm list known
```

```bash
rvm install 2.4
```

```bash
rvm use 2.4 --default
```

## Gem 安装 Jekyll

```bash
gem install jekyll jekyll-paginate jekyll-assets kramdown
```

## 参考

[RVM (rvm.io)](https://rvm.io/)
[Install Ruby 2.4 (theshell.guru)](https://www.theshell.guru/install-ruby-2-4-centos-7-3/)
