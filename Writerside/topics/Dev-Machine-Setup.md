# Dev Machine Setup
Useful reminders for setting up a new development laptop. 

## Bash profile setup
Add the following to the .bashrc

```Bash
PS1='\[\033[0;32m\]\[\033[0m\033[0;32m\]\u\[\033[0;36m\] @ \[\033[0;36m\]\h \w\[\033[0;32m\]\n\[\033[0;32m\]└─\[\033[0m\033[0;32m\] \$\[\033[0m\033[0;32m\] ▶\[\033[0m\] '
```

## Git Prompt
Use the prompt available at [Git Prompt](https://github.com/magicmonty/bash-git-prompt)
To override the bash prompt to look more like is produced in non-git 
directories and match the profile setup, use the following instead of the 
vanilla version from the creator.  Note the entries for START and END:

Add / Override the following in .bashrc for Linux dev machines:  
```Bash
if [ -f "$HOME/.bash-git-prompt/gitprompt.sh" ]; then
    GIT_PROMPT_ONLY_IN_REPO=1
    GIT_PROMPT_START='\[\033[0;32m\]\[\033[0m\033[0;32m\]\u\[\033[0;36m\] @ \[\033[0;36m\]\h \w\[\033[0;32m\]'
    GIT_PROMPT_END='\n\[\033[0;32m\]└─\[\033[0m\033[0;32m\] \$\[\033[0m\033[0;32m\] ▶\[\033[0m\] '
    source "$HOME/.bash-git-prompt/gitprompt.sh"
fi
```

Add / Override the following .bash_profile for macOS:  
```Bash
if [ -f "$(brew --prefix)/opt/bash-git-prompt/share/gitprompt.sh" ]; then
  __GIT_PROMPT_DIR=$(brew --prefix)/opt/bash-git-prompt/share
  GIT_PROMPT_ONLY_IN_REPO=1
  GIT_PROMPT_START='\[\033[0;32m\]\[\033[0m\033[0;32m\]\u\[\033[0;36m\] @ \[\033[0;36m\]\h \w\[\033[0;32m\]'
  GIT_PROMPT_END='\n\[\033[0;32m\]└─\[\033[0m\033[0;32m\] \$\[\033[0m\033[0;32m\] ▶\[\033[0m\] '
  source "$(brew --prefix)/opt/bash-git-prompt/share/gitprompt.sh"
fi
```
Note that the above is what was created when Homebrew was used to install the 
Git prompt, just edited to keep the same bash prompt.

## Git Ignore
See the note on Git Ignore File for detailed instructions


