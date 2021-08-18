# Scripts to run after installing ubuntu.



### Setup Proxy 
```bash
gsettings set org.gnome.system.proxy mode 'manual'
gsettings set org.gnome.system.proxy.http host 'http://userName:password@proxy'
gsettings set org.gnome.system.proxy.http port port
gsettings set org.gnome.system.proxy.ftp host 'http://userName:password@proxy'
gsettings set org.gnome.system.proxy.ftp port port
gsettings set org.gnome.system.proxy.https host 'http://userName:password@proxy'
gsettings set org.gnome.system.proxy.https port port

echo 'export http_proxy="http://userName:password@proxy:port";'  | tee -a ~/.bashrc
echo 'export https_proxy="http://userName:password@proxy:port";' | tee -a ~/.bashrc
echo 'export HTTPS_PROXY="http://userName:password@proxy:port";' | tee -a ~/.bashrc
echo 'export HTTP_PROXY="http://userName:password@proxy:port";'  | tee -a ~/.bashrc
source ~/.bashrc


sudo snap set system proxy.http="http://userName:password@proxy:port"
sudo snap set system proxy.https="http://userName:password@proxy:port"



sudo touch /etc/apt/apt.conf|| exit
echo 'Acquire::http::proxy "http://userName:password@proxy:port";'  | sudo tee -a /etc/apt/apt.conf
echo 'Acquire::https::proxy "http://userName:password@proxy:port";'  | sudo tee -a /etc/apt/apt.conf
echo 'Acquire::ftp::proxy "http://userName:password@proxy:port";'  | sudo tee -a /etc/apt/apt.conf


echo 'Acquire::http::proxy "http://userName:password@proxy:port";'  | sudo tee -a /etc/environment
echo 'Acquire::https::proxy "http://userName:password@proxy:port";'  | sudo tee -a /etc/environment
echo 'Acquire::ftp::proxy "http://userName:password@proxy:port";'  | sudo tee -a /etc/environment
```


### Update packages
```bash
sudo apt update
sudo apt dist-upgrade
```


### Download and install latest google chrome
```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
```





### Install necessary packages
```bash
sudo apt-get install ubuntu-restricted-extras vlc uget gfortran gnuplot python3-pip vim python-dev htop git gnome-tweak-tool openssh-server okular libatlas-base-dev liblapack-dev libblas-dev net-tools sqlite3 openmpi-bin curl
```



### Install necessary python packages
```
pip install numpy scipy h5py matplotlib pandas nose setuptools sympy ipython jupyter dash
```



### Install and setup intel oneApi
#### Add the repo
```bash
wget https://apt.repos.intel.com/intel-gpg-keys/GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB
sudo apt-key add GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB
rm GPG-PUB-KEY-INTEL-SW-PRODUCTS.PUB

echo "deb https://apt.repos.intel.com/oneapi all main" | sudo tee /etc/apt/sources.list.d/oneAPI.list
```
#### Install intel oneApi
```bash 
sudo apt install intel-basekit intel-hpckit 
```
#### Setup oneApi, activate environment
run this command
```bash
source /opt/intel/oneapi/setvars.sh
```
or add this to `~/.bashrc`
```bash
. /opt/intel/oneapi/setvars.sh  &>/dev/null
```
#### Selectively activate environment
Save a configuration file e.g. save following,
```
default=exclude
compiler=latest
mkl=latest
intelpython=latest
mpi=latest
```
in a file named `configFile.txt`, and source the `setvars.sh`
```
source /opt/intel/oneapi/setvars.sh --config=configFile.txt &> /dev/null
```
to activate only C,C++,Fortran,Python and MPI.



### Install LaTeX
Install the full latex package
```bash
sudo apt install texlive-full
```
if you don't need the full then just instll 
```bash
sudo apt instll texlive-latex-extra
```
Install `texmaker`
```bash
sudo apt-get install texmaker
```
or install the `texstudio`
```bash
sudo -E add-apt-repository ppa:sunderme/texstudio
sudo apt-get install texstudio
```




### Install fuzzy search
```bash
git clone --depth 1 https://github.com/junegunn/fzf.git ~/.fzf
~/.fzf/install
source ~/.bashrc
```


### Random tweaks
Set 12h clock format
```bash
gsettings set org.gnome.desktop.interface clock-format 12h
```
Isolate application workspaces
```bash
gsettings set org.gnome.shell.extensions.dash-to-dock isolate-workspaces true
```
Show weekday in clock
```bash
gsettings set org.gnome.desktop.interface clock-show-weekday true
```
Show seconds in clock
```bash
gsettings set org.gnome.desktop.interface clock-show-seconds true
```
Set Ctrl-Tab to change tabs in terminal
```bash
gsettings set org.gnome.Terminal.Legacy.Keybindings:/org/gnome/terminal/legacy/keybindings/ next-tab '<Primary>Tab'
gsettings set org.gnome.Terminal.Legacy.Keybindings:/org/gnome/terminal/legacy/keybindings/ prev-tab '<Primary><Shift>Tab'
```