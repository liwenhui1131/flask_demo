[flask中文文档](https://dormousehole.readthedocs.io/en/latest/tutorial/)
### 运行
linux 

    export FLASK_APP=flaskr
    export FLASK_ENV=development
    flask run
Windows

    set FLASK_APP=flaskr
    set FLASK_ENV=development
    flask run

Windows PowerShell

    flaskr目录上级中运行
    $env:FLASK_APP = "flaskr"
    $env:FLASK_ENV = "development"
    flask run

### 初始化数据库文件
    flask init-db
    Initialized the database

### 项目可安装化

#### 描述项目
> setup.py 文件描述项目及其从属的文件。MANIFEST.in文件说明include_package_data函数需要包含的静态文件。更多内容和参数参见
[官方打包指南](https://packaging.python.org/tutorials/packaging-projects/) 

<pre>
# setup.py
from setuptools import find_packages, setup
setup(
    name='flaskr',
    version='1.0.0',
    packages=find_packages(),
    include_package_data=True,
    zip_safe=False,
    install_requires=[
        'flask',
    ],
)
# MANIFEST.in
include flaskr/schema.sql
graft flaskr/static
graft flaskr/templates
global-exclude *.pyc
</pre>

#### 安装项目
    pip install -e .

### 部署产品
构建和安装

    pip install wheel
    python setup.py bdist_wheel
    pip install flaskr-1.0.0-py3-none-any.whl
    export FLASK_APP=flaskr
    flask init-db
配置密钥

    cd venv/var/flaskr-instance/
    > config.py
    echo "SECRET_KEY = b'_5#y2L"F4Q8z\n\xec]/'" >config.py
运行

    pip install waitress
    waitress-serve --call 'flaskr:create_app'
    Serving on http://0.0.0.0:8080