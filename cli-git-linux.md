
# git
## configuracion de git con ssh
Tener instalado git en el sistema linux para verificar si lo tiene instalado

```bash
git --version
```

si no lo tiene, el comando siguiente es para instalarlo

```bash
sudo apt install git -y
```
pasos para la configuracio de git en el sistema linux

- configuracion del nombre
```bash
git config --global user.name "nombreuserdegithub"
```
- configuracion del correo
```bash
 git config --gobal user.email correoasocidocongithub@gmail.com
 ```

- para ver la configuracion general
```bash
git config --list
```
## configuracion con ssh
instalar el agente ssh
```bash
sudo apt install keychain
```
para ver si tenemos en el sistema un clave ssh

```bash
ls -al ~/.ssh
```

para crear un clase ssh con el correo asociado a github en home de usuario

```bash
ssh-keygen -t ed25519 -c "corereogit"
```

para entrar en la caperta .ssh
```bash
cd .ssh
```
alli podemos listar las configuraciones si tenemos una clave ssh

que son las las dos claves la privada y la publica la que nos va servir va ser la publica

Verificar que shell tiene en su terminal, con el comando
```bash
echo $SHELL
```
si zsh o bash

para bash es
```bash
nano ~/.bashrc
```

para zsh
```bash
nano ~/.zshrc
```
colocar la siguiente configuracion en al final de la configuracion de la shell
```bash
#configuracion de sshgit
eval "$(keychain -q --eval --agents ssh ~/.ssh/id_ed25519)"
```
para recargar la configuracion de la shell de su terminal bash o zsh
```bash
source ~/.bashrc
```
```bash
source ~/.zshrc
```
ir a la repositorio en apartado settigs para la configuracion ssh

imagen falta por agregar

Despues ir a la parte de SSH and GPD keys

- SSH KEYS
crear nueva ssh, donde se les mostrar un pequeño formulario con los campos de titulo, el tipo de key y la key que se genero con ssh-keygen que se encuentra en el directorio .ssh que es la clave publica.
la primera configuracion el tipo de key es la la authentication key con la clave publica

la segudo configuracion es la firma, el tipo de key es la Signing Key igual el titulo, y la clave publica.

## contra configuracion de git
En el directorio cd .config/git/
el archivo llamando config

ingresar la siguiente configuracion:
```bash
[user]
  name = nombreusergithub
  email = correodegithu
  signingkey = contenido_clave_ssh_publica
[commit]
  gpgsign = true
[gpg]
  format = ssh
[push]
  autoSetupRemote = true
[alias]
  gone = ! git fetch -p && git for-each-ref --format '%(refname:short) %(upstream:track)' | awk '$2 == \"[gone]\" {print $1}' | xargs -r git branch -D
  rmcache = rm -rf --cached .
[core]
  editor = nvim
  autocrlf = false
  pager = cat
[init]
  defaultBranch = main
[pull]
  rebase = false
[merge]
  tool = nvimdiff
[mergetool]
  keepBackup = false
[mergetool "nvimdiff"]
  cmd = nvim "$MERGED"
[alias]
  subup = submodule update --init --recursive
  co = checkout
  cob = checkout -b
  br = branch
  st = status
  cm = commit -m
  amend = commit --amend -m
  po = push origin
  cp = cherry-pick
```