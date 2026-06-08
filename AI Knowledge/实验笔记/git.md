-  将项目上传到GitHub仓库[[2026.5.6#^985352]]
- 更新git
	```
	git add .
	git commit -m "描述这次改变了什么"
	git push  
	```
	==git push 把刚才commit的这个版本上传到远程的GitHub仓库上，第一次push需要git push -u origin main  以后就不用了==  

- [ ] 忽略某个文件夹的上传
      创建.gitignore.txt   
      里面写上temp/  则可以忽略temp文件夹里的内容
      -  但是如果该项目已经被跟踪过，只写gitignore是不行的，需要先清楚跟踪
        运行git rm -r --cached 文件夹名   
- [ ] 从github上面clone我的仓库  
      git clone https://github.com/hyhyyh66/my_biyelunwen.git   
      git pull 
      这句话相当于把一整个项目给克隆下来了  要在你决定把这个项目放到那个文件夹下面的路径使用
    ==只会clone有的文件夹 不会改变你现存的文件夹等== 
    ==只有第一次用clone  接下来都用pull即可==