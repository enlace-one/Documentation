
# Git Ignore
Make a file like the below in the applicable directory or a parent in the repo.
```
.gitignore
```
Here is a sample for Django
```
# Django/Python #
*.log
*.pot
*.pyc
__pycache__
db.sqlite3
media

# Backup files # 
*.bak 

# Distribution / packaging 
.Python build/ 
develop-eggs/ 
dist/ 
downloads/ 
eggs/ 
.eggs/ 
lib/ 
lib64/ 
parts/ 
sdist/ 
var/ 
wheels/ 
*.whl
*.egg-info/ 
.installed.cfg 
*.egg 
*.manifest 
*.spec 

# Jupyter Notebook 
.ipynb_checkpoints 

# Environments 
.env 
.venv 
env/ 
venv/ 
ENV/ 
env.bak/ 
venv.bak/ 

# Visual Studio Code # 
.vscode/* 
!.vscode/settings.json 
!.vscode/tasks.json 
!.vscode/launch.json 
!.vscode/extensions.json 
.history
```