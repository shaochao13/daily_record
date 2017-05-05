1. 用来设置git的用户名  
        
        git config --global user.name "Albert"   

    可以查看已设置的用户  

        git config --global user.name 

2. 用来设置git上的邮箱账号    
        
        git config --global user.email "...." 

    可以查看已经设置的邮箱账号 

        git config --global user.email 

3. 创建仓库     
        
        git init 

4. 把想要添加到git仓库中 
        
        git add 文件名或文件夹名 

5. 真正地把文件添加到git仓库中去。    
        
        git commit -m "....." 

6. 取消添加     
        
        git reset  

7. 查看哪些文件修改 
        
        git status  

8. 查看一个文件具体的改动  
    
        git diff 文件名  

9. 查看提交记录   
    
        git log     

10. 创建一个名为version1.0的分支 
    
        git branch version1.0  

    查看已创建好的分支   
        
        git branch  

11. 用来在各个版本之间切换，作用是使修改的代码在哪个版本上生效。  
        
        git checkout + 版本号 

12. 合并分支上修改的BUG或者代码到master 主线： 

    第一步： 切换到主线 master上。 

        git checkout master
    
    第二步： 执行命令： 

        git merge version1.0  --- version1.0 为想要合并的分支版本号

13. 删除分支: 
    
        git branch -D  version1.0  ---- 作用会将version1.0版本号的分支从git中删除掉。

14. 将本地修改 同步到远程版本库上：

        git push origin master
    `origin` 指定的是远程版本库的git地址，`master`指定的是同步到哪一个分支上。

15. 将远程版本库上的修改同步到本地：

    第一种：使用 `fetch` 命令：

        git fetch origin master

    此时同步下来的修改并不会合并到任何分支上，而是会存放到一个`origin/master` 分支上，此时可以使用 

        git diff origin/master

    查看远程版本库上到底修改了什么。之后再使用`merge` 命令将`origin/master`分支上的修改合并到主分支上即可。

        git merge orgin/master

    第二种：使用 `pull` 命令：

        git pull origin master 

    将远程版本库上获取最新的修改合并到本地库中。