# 一群大白菜前端组织教程及规范

欢迎大家加入我们的学习组织，大家一起学习一起进步~有问题可以提`issue`或者在群里问

## git简明教程

第一次接触git的新手请看这篇教程，并根据教程走一遍。 [菜鸟教程](http://www.runoob.com/w3cnote/git-guide.html)

### git规范

#### 代码库分类

- 主库：位于github服务端，所有开发的代码最终都要合到主库。
- 个人代码库（服务端）：从主库fork出来，位于服务端。每个人自已开发的代码，由本地的git库push到每个人自己的个人代码库（服务端），再由个人代码库（服务端）合入主加。
- 个人工作库：位于每个开发人员的开发机器，从个人代码库（服务端）clone到本地。每个开发人员开发的代码，先commit到个人工作库，再由个人工作库push到个人代码库（服务端）。

#### 人员角色分类
- Owner：拥有主库的所有权限。
- Committer：具有将开发人员的合并需求（MR）合入主库的权限。基于安全考虑，我们设置为只能通过MR的方式将代码合入主库，而不能直接push到主库。
- Developer：只能从自己的个人代码库（服务端）提交合并代码的请求（MR），是否能够合入，由Committer进行审核。

#### 基本流程

1. 开发人员从主库fork出自己的个人代码库。
2. 开发人员将自己的个人代码库clone到本地，即个人工作库。
3. 开发人员在开发了新代码后（包括新增和修改），先将代码commit到自己的个人工作库，再由个人工作库push到个人代码库。
3. 开发人员提交从个人工作库到主库的MR，Committer审核后，决定是否将MR合入主库。
4. 每个开发人员从主库pull最新代码到个人工作库。


#### 活动分支合入主分支时发生冲突

##### 产生原因
平时基于活动分支开发，如果这个过程中为了修复bug而拉了一个bugfix分支，当bugfix分支开发完成并合入master分支后，如果bugfix分支和活动分支修改了相同的文件，则在活动分支合入master分支时就会产生冲突。

##### 解决方法
- 从个人代码库（服务端）clone一个库到本地，即专门用于合并的个人工作库。（也可以用之前的个人工作库，但初学都容易混淆，建议单独clone一个。）
- 从主库的活动分支上pull最新的代码到本地。
- 从主库的master分支上pull最新的代码到本地。
- 此时会产生冲突，手工修复冲突，然后先commit到本地的个人工作库，再push到个人代码库（服务端）。
- 提交从个人工作库（服务端）到主库的MR（此时不会再有冲突），然后由Committer审核后将MR合入主库。

## 开发工具及流程中常见问题解决方案

> 有飞墙软件的同学可以在开发过程中打开，避免一些因为墙高导致的问题产生。

### node

开发之前请确保你已经安装了node环境。
[node的下载和安装](https://note.youdao.com/)

### `yarn` 包管理工具

`Yarn` 缓存了每个下载过的包，所以再次使用时无需重复下载。同时利用并行下载以最大化资源利用率，因此安装速度更快。

[Yarn中文网有相关下载安装和说明](https://yarn.bootcss.com/)

> `yarn` 不是必须的，有兴趣的同学或者在使用 `npm` 的时候产生问题了可以安装和使用。

### 遇到部分包安装出现问题？

1. 使用 `cnpm` 替代 `npm`

```
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

2. 使用 `nrm` 管理 `npm`

```
$ npm install -g nrm

$ nrm ls

  npm ---- https://registry.npmjs.org/
* cnpm --- http://r.cnpmjs.org/
  taobao - https://registry.npm.taobao.org/
  nj ----- https://registry.nodejitsu.com/
  rednpm - http://registry.mirror.cqupt.edu.cn/
  npmMirror  https://skimdb.npmjs.com/registry/
  edunpm - http://registry.enpmjs.org/

$ nrm use taobao
  
$ npm install
```