# Guide to install Anaconda and get started with conda

## Install Anaconda on Mac OS
Download the command-line version of the [macOS installer](https://www.anaconda.com/downloads#macos) for your system.

For pythone 3.7 enter the following:
```
$ bash ~/Downloads/Anaconda3-2019.03-MacOSX-x86_64.sh 
```

## Getting started with conda
When you begin using conda, you already have a default environment named `base`. You don't want to put programs into your base environment, though. Create separate environment to keep your programs isloated from each other. 
The following command will create a new environment named `adhoc` that contains Python 3.7 and install all of default Anaconda packages. 
```
(base) $ conda create --name adhoc python=3.7 anaconda
```

To use, or activate the new environment, type the following (The active environment will be displayed in front of your prompt) :
```
(base) $ conda activate adhoc
(adhoc) $
```

To see a list of all your environments, type:
```
(adhoc) $ conda info --envs
conda environments:
base                     /Users/inbumsung/anaconda3
adhoc                 *  /Users/inbumsung/anaconda3/envs/adhoc
```

Verify which version of Python is in your current environment:
```
(adhoc) $ python --version
Python 3.7.3
```

Deactivate the current environment and return to base environment:
```
(adhoc) $ conda activate
(base) $
```

To remove an `adhoc` environment, run:
```
(base) $ conda remove --name adhoc --all
```
