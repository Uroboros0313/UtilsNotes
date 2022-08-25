# 本地创建新分支并提交远程

- 新建分支      
`git branch <your_branch_name>`

- 查看所有分支       
`git branch -a`

- 查看与远程分支联系的本地分支          
`git branch  -vv `

- 切换到新分支         
`git checkout <your_branch_name>`

- 添加更改        
`git add .`             
`git commit -m "your_comments"`       
`git status`

- 推送远程分支       
`git push origin <your_branch_name>`

- 查看当前用户名与邮箱          
`git config user.name`        
`git config user.email`

- 修改当前用户名与邮箱          
`git config --global user.name <new_name>`        
`git config --global user.email <new_email>`