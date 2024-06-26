# 配置自己的 GitLab 账号（队长&队员）

按照主办方的提示，从 cg 平台进入 GitLab 并创建你的 GitLab 账号。  
接下来做以下操作。

## 获取 Access Token

由于这个比赛不支持 SSH 推拉代码，故我们采取 Access Token + 本地长期缓存的方式方便推拉代码。

在赛事 GitLab 中点击右上家头像 -> Preferences。点击左侧 Access Tokens。勾选所有权限，创建一个 Access Token。

<img src="assets/config_self_gitlab_01.png" alt="Config" width="500"/>

复制这个 Access Token，保存下来，推代码的时候会用到。

## 配置 Git

在你配置好的环境中（按照主办方要求配置使用虚拟机或者WSL，当然经过测试 Mac OS 的 Clang 那一套都可以兼容），配置你的 Git 信息。

```bash
git config --global user.name "你的名字"
git config --global user.email "你的邮箱地址"
```

这将用于提交代码时的作者信息。

### 登录凭据保存

以下三种方式选择一种即可。

#### git credential.helper
启用长期保存凭据，之后推代码时只需要输入一次 Access Token 即可自动记住。

```bash
git config --global credential.helper store
```

#### 在URL中置入登录账号密码

此种方法需要修改克隆时的URL，在地址前面加入形如“用户名:密码@"格式的登录信息。

```bash
git clone https://<username>:<access_token>@gitlab.eduxiji.net/csc1/nscscc/compiler2024.git
```

- 这种方法一次只能设置一个仓库
- 已经克隆到本地的仓库可以修改仓库中的`.git/config`

#### $HOME/.netrc

通过 `$HOME/.netrc` 配置文件自动登录，适用于同时配置多个仓库的情况。
```bash
nano ~/.netrc
```

```bash
# educg selfhosted gitlab
machine gitlab.eduxigi.net
login <USER_NAME_HERE>
password <ACCESS_TOKEN_HERE>
```
