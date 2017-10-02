## ----------------------------------------------------------------------------\
# Setting prompt with user@host path(relative to HOME) and
# git branch if available). With colors.
# ----------------------------------------------------------------------------|
# git-track
function parse_git_branch {
git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/\1/'
}
function git-track {
CURRENT_BRANCH=$(parse_git_branch)
git-config branch.$CURRENT_BRANCH.remote $1
git-config branch.$CURRENT_BRANCH.merge refs/heads/$CURRENT_BRANCH
}
function parse_git_branch_and_add_brackets {
git branch --no-color 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/\ \[\1\]/'
}
PS1="\[\e[31;1m\]\u@\[\e[36;1m\]\h: \[\033[0;32m\]\$(parse_git_branch_and_add_brackets) \[\033[0m\] \[\e[32;1m\]\w$ \[\e[0m\]"
# ----------------------------------------------------------------------------/
