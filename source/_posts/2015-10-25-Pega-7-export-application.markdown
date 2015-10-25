title:  Pega 7如何导出应用程序
date: 2015-10-25 16:47:19
updated: 2015-10-25 16:47:24
comments: true
tags: pega
categories: pega
---

> Pega版本：Pega 7.1.8

## 前言

当我们在Pega 7中完成一个应用程序后怎么把应用程序导出来并发给其他人呢？

## 操作步骤

### 打开应用导出页面

点击左上角DesignerStudio图标，依次选择Application -> Distribution -> Export

![application-export-menu](application-export-menu.png)

### 配置导出参数

在导出模式中选择Product

![export-preference-export-mode](export-preference-export-mode.png)

在产品列表中选择我们自己建的应用

![export-preference-product](export-preference-product.png)

在版本列表中选择最新的版本

![export-preference-version](export-preference-version.png)

给导出的文件起一个名字，例如我的命名规则：应用名 + "_" + 8位日期

![export-preference-file-name](export-preference-file-name.png)

### 锁定RuleSet

点击“执行导出”按钮后会出现如下提示：
> 这个Product涉及未锁定的RuleSet版本实例，请使用下面链接锁定它们或更新你的Product rule以允许导出未锁定的版本。如果在Product rule中勾选了允许导出未锁定版本的RuleSet，请确保你保存了该Product rule，否则不会生效。

![export-warning](export-warning.png)

依次点开提示中的链接后点击“Lock and Save”锁定RuleSet版本

![lock-rule-set](lock-rule-set.png)

### 设置Product rule

**注意**：如果你已经锁定了RuleSet（[锁定RuleSet](#锁定RuleSet)）则无需此操作

打开左侧的Records面板，依次点开SysAdmin -> Product，找到我们要导出的Product对应的Product rule

![find-product-rule](find-product-rule.png)

在Product rule的底部勾选“Allow unlocked ruleset versions?”然后保存

![product-rule](product-rule.png)

### 导出应用

设置完成后就可以导出应用了

点击“执行导出”按钮，耐心等待，导出完成后会出现一个链接，右键另存为即可保存导出的应用到本地

![export-product](export-product.png)

