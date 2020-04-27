#####Git 分支设计规范

##### 环境说明
```
   DEV 环境：用于开发者调试使用。
   FAT 环境：功能验收测试环境，用于测试环境下的软件测试者测试使用。
   UAT 环境：用户验收测试环境，用于生产环境下的软件测试者测试使用。
   PRO 环境：就是生产环境。

   比如，项目域名为：http://www.abc.com，那么相关环境的域名可这样配置：
   
   DEV 环境：本地配置虚拟域名即可
   FAT 环境：http://fat.abc.com
   UAT 环境：http://uat.abc.com
   PRO 环境：http://www.abc.com
```

##### 分支
|分支前缀 |名称 | 环境 | 可访问|
|---- | ----| ---- |----|
|master | 主分支 | PRO | Y|
|release| 预上线 | UAT | Y|
|hotfix | 紧急修复| DEV | N|
|develop | 测试   |FAT  | Y|
|feature | 需求开发 | DEV | N|

    master 为主分支，用于部署到正式环境（PRO），一般由 release 或 hotfix 分支合并，任何情况下不允许直接在 master 分支上修改代码。

    release 为预上线分支，用于部署到预上线环境（UAT），始终保持与 master 分支一致，一般由 develop 或 hotfix 分支合并，不建议直接在 release 分支上直接修改代码。
    如果在 release 分支测试出问题，需要回归验证 develop 分支看否存在此问题。

    hotfix 为紧急修复分支，命名规则为 hotfix- 开头。
    当线上出现紧急问题需要马上修复时，需要基于 release 或 master 分支创建 hotfix 分支，修复完成后，再合并到 release 或 develop 分支，一旦修复上线，便将其删除。

    develop 为测试分支，用于部署到测试环境（FAT），始终保持最新完成以及 bug 修复后的代码，可根据需求大小程度确定是由 feature 分支合并，还是直接在上面开发。一定是满足测试的代码才能往上面合并或提交。

    feature 为需求开发分支，命名规则为 feature- 开头，一旦该需求上线，便将其删除。

#####Commit 日志规范
    提交信息一定要认真填写！

***建议参考规范：`<type>(scope)：<subject>`***

    比如：fix(首页模块)：修复弹窗 JS Bug。

    type 表示 动作类型，可分为：
    fix：修复 xxx Bug
    feat：新增 xxx 功能
    test：调试 xxx 功能
    style：变更 xxx 代码格式或注释
    docs：变更 xxx 文档
    refactor：重构 xxx 功能或方法
    scope 表示 影响范围，可分为：模块、类库、方法等。

    subject 表示 简短描述，最好不要超过 60 个字，如果有相关 Bug 的 Jira 号，建议在描述中加上。
