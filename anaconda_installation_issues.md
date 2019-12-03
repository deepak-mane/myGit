# Anaconda Installation Issues


### 1. SSL Handshake issue when executing ```conda update conda```
- Run git bash as admin
- conda config --set ssl_verify False
- execute ``` conda update conda ```
- can try also doing
  - download cacert.pem from https://curl.haxx.se/ca/cacert.pem, save to c:\Cmder\cacert.pem
  - open, c:\Cmder\config\user-profile.sh
  - add this line, ... export REQUESTS_CA_BUNDLE=/c/Cmder/cacert.pem ...
  - run, Cmder ->new console -> {bash::bash as Admin}

### 2. Creating new env with specific python version only else navigator is not available
```
conda update conda
conda create -n myenv python=3.6
conda activate myenv
conda install anaconda-navigator
conda install navigator-updater
```
