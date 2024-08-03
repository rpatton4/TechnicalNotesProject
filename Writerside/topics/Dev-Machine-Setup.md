# Dev Machine Setup
Useful reminders for setting up a new development laptop. 

## Bash profile setup
Add the following to the .bashrc

```Bash
PS1='\[\033[0;32m\]\[\033[0m\033[0;32m\]\u\[\033[0;36m\] @ \[\033[0;36m\]\h \w\[\033[0;32m\]$(__git_ps1)\n\[\033[0;32m\]└─\[\033[0m\033[0;32m\] \$\[\033[0m\033[0;32m\] ▶\[\033[0m\] '
```

## Git Prompt
Use the prompt available at [Git Prompt](https://github.com/magicmonty/bash-git-prompt)
To override the bash prompt to look more like is produced in non-git directories and match the profile setup,
use the following instead of the vanilla version from the creator.  Note the entries for START and END:

```Bash
if [ -f "$HOME/.bash-git-prompt/gitprompt.sh" ]; then
    GIT_PROMPT_ONLY_IN_REPO=1
    GIT_PROMPT_START='\[\033[0;32m\]\[\033[0m\033[0;32m\]\u\[\033[0;36m\] @ \[\033[0;36m\]\h \w\[\033[0;32m\]'
    GIT_PROMPT_END='\n\[\033[0;32m\]└─\[\033[0m\033[0;32m\] \$\[\033[0m\033[0;32m\] ▶\[\033[0m\] '
    source "$HOME/.bash-git-prompt/gitprompt.sh"
fi
```



