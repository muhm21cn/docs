# 配置 Git

## 1.克隆 Git 仓库

flow.ci 通过 [git clone](https://github.com/flowci-plugins/gitclone) 插件来实现 clone 代码.

```yaml
steps:
- name: clone
  docker:
    image: flowci/debian-git ## 也可使用带有 git 命令的其他 image
  plugin: 'gitclone'
```

具体仓库地址，可以通过 YAML 或者 UI 界面的方式定义。如果 URL 为 SSH 协议，请参考下一节 [访问权限](##2.访问权限)

- YAML 配置

  ```yaml
  envs:
    FLOWCI_GIT_URL: "https://github.com/FlowCI/spring-petclinic-sample.git"
    # FLOWCI_GIT_CREDENTIAL: your_secret_name, created from secret from Admin Settings -> Secrets -> +
  ```

- UI 界面配置

  ![git vars](../../src/git/git_settings.png)

## 2.访问权限

如果 Git 链接为 SSH 协议，例如 `git@github.com:FlowCI/docs.git`, 则需要配置 SSH-RSA 秘钥已获得代码的访问权限.

1. 创建 SSH-RSA 秘钥

   - 进入管理员界面 `Settings -> Secret -> +`
   - 输入一个秘钥名称， 例如 `ras-test`
   - 选择 `SSH key` 类型
   - 点击生创建新的秘钥，或者 copy 已有的公钥私钥
   - 保存

    ![how to create ssh-rsa secret](../../src/secret/create_ssh_key.gif)

2. 配置秘钥到工作流

   `FLOWCI_GIT_CREDENTIAL` 用于 [Git clone 插件](https://github.com/flowci-plugins/gitclone) 指定用哪个秘钥访问，例如可在 YAML 中设置该变量为秘钥名称。

   ```yaml
    envs:
      FLOWCI_GIT_CREDENTIAL: "rsa-test"

    steps:
    - name: clone
      docker:
        image: flowci/debian-git
      plugin: 'gitclone'
   ```

## 3.Git 仓库中添加访问权限，及触发事件

不同 Git 仓库的访问权限，和触发事件的配置有略微差异，目前 flow.ci 支持的仓库有

- [GitHub](./github.md)
- [GitLab](./gitlab.md)
- [Gogs](./gogs.md)
- [Gitee](./gitee.md)

请点击相关 Git 仓库查看详细配置方法
