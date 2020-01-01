# Ubuntu 18.04 Orientation

Install the below packages after you have install Ubunut 18.04
[Setting Up Ubuntu on VM ](https://dev.to/awwsmm/setting-up-an-ubuntu-vm-on-windows-server-2g23)

```sh
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install net-tools tree git openssh-server ifupdown ssh curl yum -y
sudo apt-get install make build-essential libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev libsqlite3-dev wget libncurses5-dev libncursesw5-dev \
    llvm xz-utils tk-dev libffi-dev liblzma-dev -y
sudo apt-get install gcc make

```
The best way to install Vim on Unix is to use the sources. This requires a compiler and its support files. Compiling Vim isn't difficult at all. You can simply type "make install" when you are happy with the default features. Edit the Makefile in the "src" directory to select specific features.
You need to download at the sources and the runtime files. And apply all the latest patches. For Vim 6 up to 7.2 you can optionally get the "lang" archive, which adds translated messages and menus. For 7.3 and later this is included with the runtime files.

Using git is the simplest and most efficient way to obtain the latest version, including all patches. This requires the "git" command.
The explanations are on the GitHub page.

```sh
git clone https://github.com/vim/vim.git
cd vim/src
make

```
