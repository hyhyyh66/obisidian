## vscode 使用remote -ssh插件进行连接
- [ ] 相关操作
      下载完成功后 左下角有vscode 一个小图标  点击后根据指引连接服务器即可
      把环境与项目移植到服务器即可直接通过ssh操作运行代码，可以在终端看相关进程
- [ ] powershell 进行ssh连接
       
      ```bash
      ssh  lll@172.17.167.177  进行服务器连接
      top  任务管理器 实时监控进程
      kill id  杀死进程
      free -h  显示内存使用量
      ```
- [ ] 使用相关命令来确保 vscode ssh连接断开后代码仍然在运行
      [[终端（cmd）运行python代码步骤#^nohup]]