#Install zsh
```
sudo apt install zsh
sudo apt-get install powerline fonts-powerline
```
# install ohmyzsh (https://github.com/ohmyzsh/ohmyzsh)
```
curl -Lo install.sh https://raw.githubusercontent.com/jijeesh/ohmyzsh/macOS/tools/install.sh
sh install.sh
```
Set up a bira theme for your Terminal - Open .zshrc File using nano editor
```
nano .zshrc
```
Find the line ZSH_THEME="robbyrussell" replace robbyrussell with bira theme in .zshrc

```
ZSH_THEME="jijeeshMacOS"
```
Change your Default Shell
```
chsh -s /bin/zsh
```
You need to set custom path to .zshrc file instead of .bashrc

```
# clone
git clone https://github.com/powerline/fonts.git --depth=1
# install
cd fonts
./install.sh
# clean-up a bit
cd ..
rm -rf fonts
Apple Terminal: Open Terminal → Preferences → Profiles → Text, click Change under Font and select MesloLGS NF family.
```
<img width="641" alt="image" src="https://user-images.githubusercontent.com/8288856/174468406-677b1bc9-9c4e-48b0-9854-c2d384647e06.png">

Change settings for vscode
How?
open vscode
open Command Pallete (Short Cut: F1)
type settings and Select Preferences: Open Settings (JSON)
Add or Edit below settings to Settings JSON file
```
"terminal.integrated.fontFamily": "Source Code Pro for Powerline",
"terminal.integrated.defaultProfile.osx": "zsh"
```
Save.
That's all

now logout and login.
# Auto suggestions
https://github.com/zsh-users/zsh-autosuggestions
Clone this repository into $ZSH_CUSTOM/plugins (by default ~/.oh-my-zsh/custom/plugins)
```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
Add the plugin to the list of plugins for Oh My Zsh to load (inside ~/.zshrc):
```
plugins=( 
    # other plugins...
    zsh-autosuggestions
)
```
# Install Krew
Krew is the plugin manager for kubectl command-line tool
installation (https://krew.sigs.k8s.io/docs/user-guide/setup/install/)
```
(
  set -x; cd "$(mktemp -d)" &&
  curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/krew.{tar.gz,yaml}" &&
  tar zxvf krew.tar.gz &&
  KREW=./krew-"$(uname | tr '[:upper:]' '[:lower:]')_amd64" &&
  "$KREW" install --manifest=krew.yaml --archive=krew.tar.gz &&
  "$KREW" update
)

export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
```
#Kubectl Plugins install via krew

```
kubectl krew install ctx
kubectl krew install ns
kubectl krew install node-shell
```

# kubectl-aliases

This repository contains [a script](generate_aliases.py) to generate hundreds of
convenient kubectl aliases programmatically.

### Examples

Some of the 800 generated aliases are:

```sh
alias k='kubectl'
alias kctx=kubectl-
alias kns=kubectl-ns

alias kgpo='kubectl get pods'
alias kdpo='kubectl describe pods'
alias krmpo='kubectl delete pods'
alias kgdep='kubectl get deployment'
alias kddep='kubectl describe deployment'
alias kgsvc='kubectl get service'
alias kdsvc='kubectl describe service'
alias kging='kubectl get ingress'
alias kding='kubectl describe ingress'
alias kgcm='kubectl get configmap'
alias kdcm='kubectl describe configmap'
alias krmcm='kubectl delete configmap'
alias kgsec='kubectl get secret'
alias kdsec='kubectl describe secret'
alias kgno='kubectl get nodes'
alias kdno='kubectl describe nodes'
alias kgns='kubectl get namespaces'
alias kdns='kubectl describe namespaces'
alias krmns='kubectl delete namespaces'
...
```

See [the full list](.kubectl_aliases).

### Installation

You can directly download the [`.kubectl_aliases` file](https://rawgit.com/jijeesh/kubectl-alias/master/.kubectl_aliases)
and save it in your $HOME directory, then edit your .bashrc/.zshrc file with:

```sh
[ -f ~/.kubectl_aliases ] && source ~/.kubectl_aliases
```

**Print the full command before running it:** Add this to your `.bashrc` or
`.zshrc` file:

```sh
function kubectl() { echo "+ kubectl $@"; command kubectl $@; }
```

### Syntax explanation

* **`k`**=`kubectl`
  * **`sys`**=`--namespace kube-system`
* commands:
  * **`g`**=`get`
  * **`d`**=`describe`
  * **`e`**=`edit`
  * **`rm`**=`delete`
  * **`a`**:`apply -f`
  * **`ex`**: `exec -i -t`
  * **`lo`**: `logs -f`
* resources:
  * **`po`**=pod, **`dep`**=`deployment`, **`ing`**=`ingress`,
    **`svc`**=`service`, **`cm`**=`configmap`, **`sec`=`secret`**,
    **`ns`**=`namespace`, **`no`**=`node`
* flags:
  * output format: **`oyaml`**, **`ojson`**, **`owide`**
  * **`all`**: `--all` or `--all-namespaces` depending on the command
  * **`sl`**: `--show-labels`
  * **`w`**=`-w/--watch`
* value flags (should be at the end):
  * **`n`**=`-n/--namespace`
  * **`f`**=`-f/--filename`
  * **`l`**=`-l/--selector`
  
### FAQ

- **Doesn't this slow down my shell start up?** Sourcing the file that contains
~500 aliases takes about 30-45 milliseconds in my shell (zsh). I don't think
it's a big deal for me. Measure it with `echo $(($(date +%s%N)/1000000))`
command yourself in your .bashrc/.zshrc.

- **Can I add more Kubernetes resource types to this?** Please consider forking
  this repo and adding the resource types you want. Not all resource types are
  used by everyone, and adding more resource types slows down shell initialization
  see above).

- **Where can I find PowerShell aliases for kubectl?** There’s a fork of this
  [here](https://github.com/shanoor/kubectl-aliases-powershell).

### Authors



-----

This is not an official Google project.
