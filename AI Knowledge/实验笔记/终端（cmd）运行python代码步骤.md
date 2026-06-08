## 每次重新打开 VS Code 后的运行流程

==先进入项目目录，再激活 conda 环境，最后运行代码。==

**第一步：进入项目目录**

```bat
cd /d D:\PRJ\BIYE_lunwen
```

**第二步：激活 convnext 环境**

```bat
D:\DEV\MiniConda\Scripts\activate.bat D:\WorkSpace\conda_envs\convnext
```

**第三步：运行项目检查**

```bat
python -m src.run_baseline --dry-run
```

**使用nohup来确保断开ssh 代码依旧在服务器上运行** ^nohup
```bat
nohup python -m src.run_baseline > train.log 2>&1 &

nohup python -m src.run_baseline --model-name convnext_tiny_se --device cuda:2 > train_se_cuda2.log 2>&1 &

nohup：断开 SSH 后继续跑
> train.log：把输出写到日志文件
2>&1：把报错也写进同一个日志
&：放到后台运行
```

