### DIRECTORY
```bash
%d  # full working directory
%/  # same as %d
%~  # working directory starting from the home dir
%x~ # same as %~but only shows x(int) amount of the lowest directories
```
### NAMES
```bash
%m  # hostname
%M  # hostname with domain extension
%n  # user
```
### FORMATING
```bash
%B # (%b) start stop bold
%U # (%u) start stop underline
%S # (%s) start stop standout mode

%F{COLOR} # (%f) start stop text color
%K{COLOR} # (%k) start stop background color
```

### DATE AND TIME
```bash
%D # date in format 2002.10.28 yy.mm.dd
%* # time in format 11.19.26 hh.mm.ss
%T # time in 24h format
%t # time in 12h format
%f # day of the month
%K # hour of day in 24h format
%L # %K in 12h format
```
### CONDITIONS
```bash
# All conditions can be used in conditional statements or as standalone
# Strings used with a '%' in front of them they may also have a integer
# infront of them else this will default to zero eg. 2- ([n][condition])
# n will default to 0

?      # true if exit code of previous command was n[default 0]
!      # whether the user is priviliged (root user --> ! == 0)
       # true if uid is n
-      # true if n shell construct started
C or / # true if the current absolute path has at least n elements
       # relative to the root directory
c . ~  # same as C but relative to home dir
D      # True if the month is equal to n (January = 0)
d      # True if the day of the month is equal to n.
e      # True if the evaluation depth is at least n.
g      # True if the effective gid of the current process is n.
j      # True if the number of jobs is at least n.
l      # True if the SHLVL parameter is at least n.
S      # True if the SECONDS parameter is at least n.
T      # True if the time in hours is equal to n
t      # True if the time in minutes is equal to n.
w      # True if the day of the week is equal to n (Sunday = 0).
```
### CONDITION STATEMENTS
```bash
## syntax %([n][condition].[trueCase].[falseCase])
## example %(!.#.$) # if user is priviliged else $

#more examples
%(!.[a].[b])# conditional equal to [a](zsh command) if host is
            # root else [b] eg%(!.#.$)
%(3?.[a].[b]) # equal to [a] if previous exit code is 3 else equal to [b]
%# # '#' if root user else %
```


### EXAMPLE

```bash
#
# custom zsh prompt that depend on whether the user is root or not
#
# ┌──(user🤖usersMBP)─[~/Desktop]
#└─$
# or
#╔══(root☠️usersMBP)─[/Users/user/Desktop]
#╠════(13:37)
#╚═#
#
if [[ $USER = "root" ]]
then
	PS1="%52F╔══(%f%F{red}%B%n%b☠️ %f%88F%m%f%52F)─[%f%248F%d%f%52F]
╠════(%T)
╚═%f%B%F{red}#%b%f "

else
	PS1="%F{cyan}┌──(%f%F{green}%B%n%b🤖%m%f%F{cyan})─[%f%2~%F{cyan}]
└─$%f "
fi
```
