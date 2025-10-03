# share

RED='$$ \e[0;31m $$'
GREEN='$$ \e[0;32m $$'
BLUE='$$ \e[0;34m $$'
YELLOW='$$ \e[1;33m $$'
NC='$$ \e[0m $$' # No Color

# Check if connected via SSH
if [ -n "$SSH_CLIENT" ] || [ -n "$SSH_TTY" ]; then
    PROMPT_COLOR=$RED
else
    PROMPT_COLOR=$GREEN
fi

# Enable __git_ps1 to show Git branch
if [ -n "$(type -t __git_ps1)" ]; then
    export GIT_PS1_SHOWDIRTYSTATE=1
    export GIT_PS1_SHOWSTASHSTATE=1
    export GIT_PS1_SHOWUNTRACKEDFILES=1
    export GIT_PS1_SHOWUPSTREAM="auto"
    PS1="${PROMPT_COLOR}\u@\h:${BLUE}\w${YELLOW}\$(__git_ps1 ' (%s)') ${PROMPT_COLOR}\$$  {NC} "
else
    PS1="${PROMPT_COLOR}\u@\h:${BLUE}\w ${PROMPT_COLOR}\  $${NC} "
fi
