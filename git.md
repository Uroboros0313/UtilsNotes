# 本地创建新分支并提交远程

- 新建分支:`git branch <your_branch_name>`

- 查看所有分支:`git branch -a`
- 查看远程和本地的所有分支:`git branch -al`
- 查看与远程分支联系的本地分支:`git branch  -vv `


- 切换到新分支:`git checkout <your_branch_name>`
- 新建并切换到新分支:`git checkout -b <your_branch_name>`

- 添加更改        
`git add .`             
`git commit -m "your_comments"`       
`git status`

- 推送远程分支(在远程仓库新建一个`<your_branch_name>`的分支)       
`git push origin <your_branch_name>`
- 从远程仓库拉取并合并到当前分支(从远程仓库拉取`<remote branch name>`的分支合并到当前分支)                  
`git pull origin <remote branch name>`

- 查看当前用户名与邮箱          
`git config user.name`        
`git config user.email`

- 修改当前用户名与邮箱          
`git config --global user.name <new_name>`        
`git config --global user.email <new_email>`

# .gitignore

.gitignore只能忽略那些原来没有被追踪的文件，如果某些文件已经被纳入了版本管理中，则修改.gitignore是无效的。        
- 解决方法: 先把本地缓存删除(改变成未被追踪状态),再提交：
```Bash
git rm -r --cached .
git add .
git commit -m 'refine codes'
git push -u origin master/main
```

## gitignore语法配置
- [ref](https://blog.csdn.net/qq_39505245/article/details/120205100?spm=1001.2101.3001.6650.2&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-2-120205100-blog-125175028.pc_relevant_3mothn_strategy_and_data_recovery&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7EBlogCommendFromBaidu%7ERate-2-120205100-blog-125175028.pc_relevant_3mothn_strategy_and_data_recovery&utm_relevant_index=3)