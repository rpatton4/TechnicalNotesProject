# Dev Machine Setup
Useful reminders for setting up a new development laptop. 

## Bash profile setup
Add the following to the .bashrc  
    export PS1='\w$(__git_ps1 " (%s)")\$ '
    PS1='\[\033[0;32m\]\[\033[0m\033[0;32m\]\u\[\033[0;36m\] @ \[\033[0;36m\]\h \w\[\033[0;32m\]$(__git_ps1)\n\[\033[0;32m\]└─\[\033[0m\033[0;32m\] \$\[\033[0m\033[0;32m\] ▶\[\033[0m\] '

## Git Prompt
Use the prompt available at [Git Prompt](https://github.com/magicmonty/bash-git-prompt)


