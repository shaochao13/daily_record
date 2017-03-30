### 文件路径操作
- os.remove(path) 或 os.unlink(path) ：删除指定路径的文件。路径可以是全名，也可以是当前工作目录下的路径。
- os.removedirs：删除文件，并删除中间路径中的空文件夹
- os.chdir(path)：将当前工作目录改变为指定的路径
- os.getcwd()：返回当前的工作目录
- os.curdir：表示当前目录的符号
- os.rename(old, new)：重命名文件
- os.renames(old, new)：重命名文件，如果中间路径的文件夹不存在，则创建文件夹
- os.listdir(path)：返回给定目录下的所有文件夹和文件名，不包括 '.' 和 '..' 以及子文件夹下的目录。（'.' 和 '..' 分别指当前目录和父目录）
- os.mkdir(name)：产生新文件夹
- os.makedirs(name)：产生新文件夹，如果中间路径的文件夹不存在，则创建文件夹

### 系统常量
- os.linesep  当前操作系统的换行符
- os.sep    当前操作系统的路径分隔符
- os.pathsep 当前操作系统的环境变量中的分隔符（';' 或 ':'）
- os.environ 存储所有环境变量的值的字典

### os.path 模块
- os.path.isfile(path) ：检测一个路径是否为普通文件
- os.path.isdir(path)：检测一个路径是否为文件夹
- os.path.exists(path)：检测路径是否存在
- os.path.isabs(path)：检测路径是否为绝对路径

- os.path.split(path)：拆分一个路径为 (head, tail) 两部分
- os.path.join(a, *p)：使用系统的路径分隔符，将各个部分合成一个路径

- os.path.abspath()：返回路径的绝对路径
- os.path.dirname(path)：返回路径中的文件夹部分
- os.path.basename(path)：返回路径中的文件部分
- os.path.splitext(path)：将路径与扩展名分开
- os.path.expanduser(path)：展开 '~' 和 '~user'
