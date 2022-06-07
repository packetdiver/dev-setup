# dev-setup
Description of my dev setup (based on my Ubuntu 22.04 LTS installation).


## [Homebrew](https://brew.sh/)

[Help](https://docs.brew.sh/Manpage)

```bash
# Prepare:
sudo apt update
sudo apt install build-essential git

# Install:
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Finish:
echo 'eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"' >> /home/marcello/.profile
eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"

```

```bash
# Test
brew doctor

# Operate:
brew --version   # check version
brew update      # gets from the Homebrew servers the information about the most recent versions of the available formulae and casks
brew outdated    # lists the outdated installed formulae and casks
brew upgrade     # upgrades the packages listed by 'brew outdated'

brew help                    # will show you the list of commands that are available
brew list                    # will show you the list of installed packages
brew search <search term>    # will list the possible packages that you can install
brew info <package name>     # will display some basic information about the package in question

brew install <package name>  # will display some basic information about the package in question
```

## [pipx](https://pypa.github.io/pipx/)

[Help](https://pypa.github.io/pipx/docs/)

```bash
# Prepare:
brew update

# Install:
brew install pipx
pipx ensurepath

# Finish:
pipx completions
eval "$(register-python-argcomplete pipx)"

# Update
brew update && brew upgrade pipx
```

## [pyenv](https://github.com/pyenv/pyenv)

[Help](https://github.com/pyenv/pyenv/wiki)

```bash
# Prepare:
brew update

# Install:
brew install pyenv


# Finish (set up shell environment for Pyenv):
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc

echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.profile
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.profile
echo 'eval "$(pyenv init -)"' >> ~/.profile

exec "$SHELL"

sudo apt-get update; sudo apt-get install make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev

# Update
brew update && brew upgrade pyenv  # update pyenv itself
```

```bash
# Operate:
pyenv install --list | less  # list all available Python versions (a lot!)
pyenv install -v pypy3.9-7.3.9  # install Pypy 3.9-7.3.9
pyenv install -v 3.10.4         # install Python 3.10.4 -> doesn't work!
env CONFIGURE_OPTS="--with-openssl=$(brew --prefix openssl@1.1) --with-openssl_rpath=auto" pyenv install 3.10.4
# but same with 3.9.13 doesn't work?!

$ pyenv versions
* system (set by /home/packetdiver/.pyenv/version)
  3.10.4
  pypy3.9-7.3.9
$ pyenv global 3.10.4
$ which python
/home/packetdiver/.pyenv/shims/python
$ pyenv versions
  system
* 3.10.4 (set by /home/packetdiver/.pyenv/version)
  pypy3.9-7.3.9
$ python -c "import ssl; print(ssl.OPENSSL_VERSION)"
OpenSSL 1.1.1o  3 May 2022
$ pyenv version
3.10.4 (set by /home/packetdiver/.pyenv/version)
```

## [GitHub CLI](https://cli.github.com/)

[Help](https://cli.github.com/manual/)

```bash
# Prepare:
brew update

# Install:
brew install gh

# Finish:
gh config set editor "code --wait"
gh config set git_protocol https

# Update
brew update && brew upgrade gh
```

```bash
# Operate:
$ gh auth login
? What account do you want to log into? GitHub.com
? What is your preferred protocol for Git operations? HTTPS
? Authenticate Git with your GitHub credentials? Yes
? How would you like to authenticate GitHub CLI? Paste an authentication token
Tip: you can generate a Personal Access Token here https://github.com/settings/tokens
The minimum required scopes are 'repo', 'read:org', 'workflow'.
? Paste your authentication token: ****************************************
- gh config set -h github.com git_protocol https
✓ Configured git protocol
✓ Logged in as packetdiver

gh repo view packetdiver/dev-setup
gh repo clone packetdiver/dev-setup
code README.md
git add .
git commit -m "my changes!"
git push origin

# Edit remote... - then local:
git pull
```


## More tools with pipx

### [ptpython](https://github.com/prompt-toolkit/ptpython)

```bash
# Prepare:
brew update && brew upgrade pipx

# Install:
pipx install ptpython
pipx inject ptpython requests

# Update
pipx upgrade ptpython
```


### [cookiecutter](https://github.com/cookiecutter/cookiecutter)

```bash
# Prepare:
brew update && brew upgrade pipx

# Install:
pipx install cookiecutter

# Update
pipx upgrade cookiecutter
```


### [jupyterlab](https://github.com/jupyterlab/jupyterlab)

```bash
# Prepare:
brew update && brew upgrade pipx
brew install pandoc
brew install texlive

# Install:
pipx install --python python3.10 jupyterlab
pipx inject jupyterlab pyppeteer   # export to Webpdf not possible? What's missing?
pipx inject jupyterlab pandas

# Update
pipx upgrade jupyterlab
```



Olther tools:
- black
- flake8
- pylint
- poetry
- isort
- pyinstaller ???
- 


