# How to install Z shell (zsh)
This documentation contains step-by-step guide on how to install zsh in Docker, with [special omz and nvim configs from Ming Rui](https://github.com/mingruimingrui/my-vim-config.git).
* Start running with Docker:
```shell
docker run --rm -it -gpus all -v $HOME:/root/$USER [dockerimagename]
```
  - `-v $HOME:/root/$USER` will mount your home directory on the server. If you do not wish the Docker to access your files on the server, remove this part.
  - You can try to run the Ubuntu 16.04 image (ubuntu:16.04) on the server, or any other image suitable on Docker hub.
  - More info on docker flags and commands can be found in [Docker documentation](https://docs.docker.com/reference/)
* Once inside Docker, run the following commands to install neccessary packages:
```shell
apt update
apt upgrade
apt install git zip wget curl zsh htop tree tmux screen g++ make cmake neovim
apt autoclean -y
apt autoremove -y
```
* Installing Ming Rui's configs:
```shell
pip install --no-cache-dir neovim jedi
git clone https://github.com/mingruimingrui/my-vim-config.git
cd my-vim-config
./setup-zsh-env.sh
./setup-vim-env.sh
cd /root
rm -rf my-vim-config
```
* Start the Z shell with `zsh`. Usually, there will be a prompt to change your default shell into zsh (enter 'yes' if you want zsh to be your default shell). Otherwise, you can change from bash to zsh with `chsh -s /bin/zsh`.
* Congrats, you're now inside zsh with omz configs!
* You can 'save' your new image and use it as a base for next time! Simply run `docker ps` to check your container ID. Then run `docker commit [containerid] [imagename]` to 'save' your new image. 
* If you want to make sure, run `docker images`. Your new image should appear there.

Have fun!
