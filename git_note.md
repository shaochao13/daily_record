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