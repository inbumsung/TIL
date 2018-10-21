# Guide to setting up and using Python3, virtualenv and jupyter notebook in macOS
The following instructions will guide you through the process of:
- installing python 3 using Homebrew
- installing virtualenv
- installing juptyer 

## View installed version of Python.
```
$ python --version
Python 2.7.10
$ which python
/usr/bin/python
```

## Install Python 3 with Homebrew.
```
$ brew install python3 # will take 2-3 minutes

$ python3 -V
Python 3.7.0
$ which python3
/usr/local/bin/python3

$ pip3 -V # pip is already installed
pip 18.0 from /usr/local/lib/python3.7/site-packages/pip (python 3.7)
```

## Install virtualenv with pip.
```
$ pip3 install virtualenv
```

## Create a new virtualenv with `virtualenv -p python3 [env_name]` command.
`virtualenv venv` command will create a folder in the current directory which will contain the python executable files, and a copy of the pip library. The name of the virtual environment can be anything; omitting the name will place the files in the current directory instead.
```
$ cd path/to/your/dev/folder/
$ virtualenv -p python3 venv 
$ ls
venv
```

## Activate the virtual environment.
```
source venv/bin/activate
```

## Install and start jupyter notebook.
```
(venv) $ python -V
python 3.6.5
(venv) $ pip install jupyter notebook
```

## Start Jupyter
```
(venv) $ jupyter notebook
```

### Deactivate virutual environment.
```
(venv) $ deactivate
$
```
