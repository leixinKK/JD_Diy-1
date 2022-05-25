<h1 align="center">
  diy机器人
  <br>
  Author: chiupam
</h1>

## 目录
- [目录](#目录)
- [仓库目录说明](#仓库目录说明)
- [版权](#版权)
- [声明](#声明)
- [特别感谢](#特别感谢)
- [简介](#简介)
- [已有功能](#已有功能)
  - [基础功能](#基础功能)
  - [可拓展功能](#可拓展功能)
  - [user.py功能](#userpy功能)
- [使用方式](#使用方式)
  - [部署自定义机器人](#部署自定义机器人)
  - [部署user.py监控机器人](#部署userpy监控机器人)
- [前瞻计划](#前瞻计划)
  - [用户要求](#用户要求)
  - [部署方法](#部署方法)
- [常用命令](#常用命令)
# 仓库目录说明
```text
JD_Diy/                     # JD_Diy 仓库
  |-- backup                    # 移除的旧文件
  |-- beta                      # 测试版机器人
  |-- config                    # 配置目录
  |-- jbot                      # 正式版机器人
  |-- module                    # 实例模块
  |-- other                     # 不便于分类脚本
  |-- pys                       # python脚本
  |-- shell                     # shell脚本
  |-- requirements.txt          # 依赖文件
@@ -47,83 +29,8 @@ JD_Diy/                     # JD_Diy 仓库
- 任何以任何方式查看此项目的人或者以直接或间接的方式使用该项目的任何脚本的使用者都应仔细阅读此声明。 本人保留随时更改或补充此免责声明的权利。一旦使用并复制或使用了任何相关脚本，则视为您已接受此免责声明。
- 您必须在下载后的24小时内从计算机或手机中完全删除以上内容。
# 特别感谢
- 脚本的写作参考了 [SuMaiKaDe](https://github.com/SuMaiKaDe) 的 [jddockerbot](https://github.com/SuMaiKaDe/bot) 仓库
- 模块的写作参考了 lxk0301 的 jd_sctipts 仓库
## 简介
随着 v4-bot 启动而启动的自定义机器人，其中大部分功能亦支持青龙用户。
## 已有功能
### 基础功能
- [x] 发送 `/start` 指令可开启自定义机器人
- [x] 发送 `/restart` 指令可重启机器人
- [x] 发送 `/help` 指令可获取快捷命令
- [x] 发送 `/install` 指令可拓展功能
- [x] 发送 `/uninstall` 指令可卸载功能
- [x] 发送 `/list` 指令列出已有功能
### 可拓展功能
- [x] 发送 `/upbot` 升级自定义机器人
- [x] 发送 `/checkcookie` 检测过期情况
- [x] 发送 `/export` 修改环境变量
- [x] 发送 `/blockcookie` 进行屏蔽操作
- [x] 发送 `pin=xxx;wskey=xxx;` 快速添加 `wskey`
- [x] 下载 `.js` `.sh` 的 `raw` 文件
- [x] 添加以 `.git` 结尾的仓库链接可添加仓库
- [x] 发送 `变量名="变量值"` 的格式消息可快捷添加环境变量
### user.py功能
- [x] 监控龙王庙频道，监控并定时执行红包雨
- [x] 关注店铺有礼自动执行（需自行配置频道ID）
- [x] 自动替换某些环境变量（需自行配置频道ID）
- [x] ~~监控动物园频道，自动下载开卡脚本并选择执行~~
# 使用方法
## 部署自定义机器人
进入容器中执行以下命令即可，此命令也可以在机器人中使用（即使用 /cmd 指令）
```shell
if [ -d "/jd" ]; then root=/jd; else root=/ql; fi
wget https://raw.githubusercontent.com/leixinKK/JD_Diy-1/main/shell/bot.sh -O $root/bot.sh
bash $root/bot.sh
```
## 部署[user.py](https://github.com/chiupam/JD_Diy/blob/main/jbot/user.py)监控机器人
首先进入容器中执行以下命令，然后按提示操作即可（此命令禁止在机器人中使用）
```shell
if [ -d "/jd" ]; then root=/jd; else root=/ql; fi; if [ -f $root/user.sh ]; then rm -f $root/user.sh; fi; cd $root; wget https://github.com/leixinKK/JD_Diy-1/main/shell/user.sh; bash user.sh
```
# 前瞻计划
测试版机器人的部署方法，功能不稳定，不建议尝试。
## 用户要求
- 比较热爱折腾
- 一定的操作基础
- 甚至可以 Pr 部分功能
## 部署方法
```shell
if [ -d "/jd" ]; then root=/jd; else root=/ql; fi; if [ -f $root/diybot_beta.sh ]; then rm -f $root/diybot_beta.sh; fi; cd $root; wget https://github.com/leixinKK/JD_Diy-1/main/shell/diybot_beta.sh; bash diybot_beta.sh
```
# 常用命令
1. 升级原机器人程序
```shell
if [ -d "/jd" ]; then root=/jd; else root=/ql; fi; if [ -f $root/bot.sh ]; then rm -f $root/bot.sh; fi; cd $root; wget https://raw.githubusercontent.com/SuMaiKaDe/bot/main/config/bot.sh; bash bot.sh
```
2. 重启程序
```shell
if [ -d '/jd' ]; then cd /jd/jbot; pm2 start ecosystem.config.js; cd /jd; pm2 restart jbot; else ps -ef | grep 'python3 -m jbot' | grep -v grep | awk '{print $1}' | xargs kill -9 2>/dev/null; nohup python3 -m jbot >/ql/log/bot/bot.log 2>&1 & fi 
```
3. 启动程序
```shell
if [ -d '/jd' ]; then cd /jd/jbot; pm2 start ecosystem.config.js; cd /jd; pm2 start jbot; else nohup python3 -m jbot >/ql/log/bot/bot.log 2>&1 & fi 
```
4. 停止程序
```shell
if [ -d '/jd' ]; then cd /jd/jbot; pm2 start ecosystem.config.js; cd /jd; pm2 stop jbot; else ps -ef | grep 'python3 -m jbot' | grep -v grep | awk '{print $1}' | xargs kill -9 2>/dev/null; fi 
```
5. 卸载diy程序
```shell
if [ -d "/jd" ]; then root=/jd; else root=/ql; fi; rm -f $root/jbot/diy/*.py
```
6. 卸载user监控程序
```shell
if [ -d "/jd" ]; then root=/jd; else root=/ql; fi; cd $root; rm -f user.session; rm -f user.session-journal; rm -f $root/jbot/diy/user.py
```
7. 重启user监控程序
```shell
if [ -d "/jd" ]; then root=/jd; else root=/ql; fi; cd $root; bash user.sh
```
8. 一键
```shell
if [ -d "/jd" ]; then root=/jd; else root=/ql; fi; if [ -f $root/bot.sh ]; then rm -f $root/bot.sh; fi; cd $root; wget https://github.com/SuMaiKaDe/bot@main/config/bot.sh; bash bot.sh; if [ -f $root/diybot.sh ]; then rm -f $root/diybot.sh; fi; cd $root; wget https://github.com/leixinKK/JD_Diy-1/main/shell/diybot.sh; bash diybot.sh; if [ -f $root/user.sh ]; then rm -f $root/user.sh; fi; cd $root; wget https://github.com/leixinKK/JD_Diy-1/main/shell/user.sh; bash user.sh
```
