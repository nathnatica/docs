
VMWARE
console mode
C+A+F1

x mode
C+A+F7

##### -print and xargs
use
find . -name xx -print0 | xargs -0 <other command>
instead of 
find . -name xx -print(is default) _ xargs <other command>
when there are posibilities of file names containing space in UNIX
or treated as seperate files 



##### exec last command
!<command>
repeats the last command

##### locate 
locate <file name>
finds file with index


##### server monitoring commands
mpstat
sudo apt-get nmon
nmon
sudo apt-get sysstat
iostat

# shows memory info
cat /proc/meminfo












apt-get install git-core 

##### update-alternatives
update-alternatives --list XX
update-alternatives --config XX


##### JDK
apt-get update
apt-get install sun-java6-jdk




##### check service list
netstat -tulpn
rcconf (of ubuntu)

sudo apt-get install xinetd
sudo apt-get install telnetd
sudo apt-get install ssh





##### SETTING TELNET
vi /etc/xinetd.d/telnet
service telnet
{
	disable = no
	flags = REUSE
	socket_type = stream
	wait = no
	user = root
	server = /usr/sbin/in.telnetd
	log_on_failure += USERID
}
sudo /etc/init.d/xinetd restart





##### SETTING BASHRC
touch .bashrc
echo "alias ll='ls -lh --color=auto'"
echo "alias la='ls -Ah --color=auto'"
echo "alias lla='ls -lAh --color=auto'"
echo "alias ltr='ls -ltrhA --color=auto'"



# .bashrc
export EDITOR=vi
export HISTCONTROL=ignoredups #ignores dups in the history 


#bash completion settings
bind "set completion-ignore-case on"
bind "set bell-style none" # no bell
bind "set show-all-if-ambigious on"

set -o vi



alias g='grep -i' # case insensitive
alias f='find . -iname' # case insensitive
alias ducks='du -cks * | sort -rn | head -11'

if [ -d ~/bin ]; then
	export PATH=:~/bin:PATH
fi 

if [ -f ~/.dirs ]; then
	touch ~/.dirs
fi
alias show='cat ~/.dirs'
save() {
	command sed "/!$/d" ~/.dirs > ~/.dirs1; \\mv ~/.dirs ~/.dirs; echo "$@"=\\"`pwd`\\" >> ~/.dirs; source ~/.dirs ;
	# or use this
	command sed "/!$/d" ~/.dirs > ~/.dirs1; mv ~/.dirs ~/.dirs; echo "$@"="`pwd`" >> ~/.dirs; source ~/.dirs ;
}
source ~/.dirs
shopt -s cdable_vars


