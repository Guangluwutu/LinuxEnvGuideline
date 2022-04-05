how to install python3.8 in server without root

step download python

`cd %DOAWNLOADPAH%`

`wget https://www.python.org/ftp/python/3.8.10/Python-3.8.10.tgz --no-check-certificate`

`tar zxvf Python-3.8.10.tgz `

step require prepare 
(openssl require intalled)

step make &install 

(openssl is dir where openssl installed) 

(python3.8.10 is dir where python will be installed)

`cd %SOURCE_PATH%`

`./configure prefix=%PATH%/python3.8.10 --with-openssl=%PATH%/openssl --enable-shared
make & make install`

step while pip

(while pip install too slow, choose demestic source) 


`清华：https://pypi.tuna.tsinghua.edu.cn/simple`

`阿里云：http://mirrors.aliyun.com/pypi/simple/`

`中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/`

`华中理工大学：http://pypi.hustunique.com/`

`山东理工大学：http://pypi.sdutlinux.org/ `

`豆瓣：http://pypi.douban.com/simple/`

for exmaple :

`pip install -i https://pypi.mirrors.ustc.edu.cn/simple/ django

`

step how to use virtualenv

`pip install virtualenv`

u can choose install global module using `--system-site-packages` or `--no-site-packages` opposite, like:

`virtualenv --system-site-packages venv`

u also can specify python version by using 
`virtualenv -p /usr/bin/python3.5  venv`

`source venv/bin/activate`

`deactivate`

