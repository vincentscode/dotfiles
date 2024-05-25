# Dotfiles

## Setting up a new machine using this repository
```bash
alias dotfiles = '/usr/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
git clone --bare https://github.com/vincentscode/dotfiles.git
dotfiles checkout
mkdir -p .config-backup
if [ $? = 0 ]; then
  echo "Checked out dotfiles.";
else
  echo "Backing up pre-existing dot files.";
  dotfiles checkout 2>&1 | egrep "\s+\." | awk {'print $1'} | xargs -I{} mv {} .config-backup/{}
fi;
dotfiles checkout
dotfiles config --local status.showUntrackedFiles no
```

## Setting up a new repository
```bash
git init --bare $HOME/.dotfiles
alias dotfiles = '/usr/bin/git --git-dir=$HOME/.dotfiles/ --work-tree=$HOME'
dotfiles config --local status.showUntrackedFiles no
dotfiles status

dotfiles add ...
dotfiles commit
dotfiles push
```
