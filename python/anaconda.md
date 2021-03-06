# 用conda创建python虚拟环境

## conda常用的命令:

    1）conda list 查看安装了哪些包。
    2）conda env list 或 conda info -e 查看当前存在哪些虚拟环境
    3）conda update conda 检查更新当前conda

## 创建python虚拟环境。

     使用 conda create -n your_env_name python=X.X（2.7、3.6等） anaconda 命令创建python版本为X.X、名字为your_env_name的虚拟环境。your_env_name文件可以在Anaconda安装目录envs文件下找到。

## 使用激活(或切换不同python版本)的虚拟环境。

    打开命令行输入python --version可以检查当前python的版本。
    使用如下命令即可 激活你的虚拟环境(即将python的版本改变)。
    Linux:  source activate your_env_name(虚拟环境名称)
    Windows: activate your_env_name(虚拟环境名称)
    这是再使用python --version可以检查当前python版本是否为想要的。

## 对虚拟环境中安装额外的包。

    使用命令conda install -n your_env_name [package]即可安装package到your_env_name中

##关闭虚拟环境(即从当前环境退出返回使用PATH环境中的默认python版本)。

   使用如下命令即可。
   Linux: source deactivate
   Windows: deactivate

## 删除虚拟环境。

   使用命令conda remove -n your_env_name(虚拟环境名称) --all， 即可删除。
## 删除环境中的某个包。

   使用命令conda remove --name $your_env_name  $package_name 即可。

# jupyter notebook选择conda环境

安装ipykernel
```bash
conda install ipykernel  
```

创建虚拟环境
```bash
conda create -n your_env_name python=X.X ipykernel
```

激活虚拟环境
```bash
activate your_env_name # windows
source activate your_env_name # linux
```

安装kernel spec 文件
```bash
python -m ipykernel install --user

# 如果要为不同环境或不同的conda 环境，需要指定唯一的名称
python -m ipykernel install --user --name your_env_name --display-name 'Python(myevn_)'
# --name 是给jupyter 启动Kernel 使用，如果指定的name已存在则会覆盖，--display-name 是为Jupyter notebook 菜单显示
```