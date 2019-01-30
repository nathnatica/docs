#### 1. Declaring an Array and Assigning values  
Unix[0]='Debian'  
Unix[1]='Red hat'  

#### 2. Initializing an array during declaration  
declare -a Unix=('Debian' 'Red hat' 'Red hat' 'Suse' 'Fedora');  

#### 3. Print the Whole Bash Array  
${Unix[@]}  

#### 4. Length of the Bash Array  
echo ${#Unix[@]}  

#### 5. Length of the nth Element in an Array  
echo ${#Unix[3]}  

#### 6. Extraction by offset and length for an array  
Unix=('Debian' 'Red hat' 'Ubuntu' 'Suse' 'Fedora' 'UTS' 'OpenLinux');  
echo ${Unix[@]:3:2}  
> Suse Fedora

#### 7. Extraction with offset and length, for a particular element of an array  
Unix=('Debian' 'Red hat' 'Ubuntu' 'Suse' 'Fedora' 'UTS' 'OpenLinux');  
echo ${Unix[2]:0:4}  
> Ubun

#### 8. Search and Replace in an array elements  
Unix=('Debian' 'Red hat' 'Ubuntu' 'Suse' 'Fedora' 'UTS' 'OpenLinux');  
echo ${Unix[@]/Ubuntu/SCO Unix}  
> Debian Red hat SCO Unix Suse Fedora UTS OpenLinux

#### 9. Add an element to an existing Bash Array  
Unix=('Debian' 'Red hat' 'Ubuntu' 'Suse' 'Fedora' 'UTS' 'OpenLinux');  
Unix=("${Unix[@]}" "AIX" "HP-UX")  

#### 10. Remove an Element from an Array  
Unix=('Debian' 'Red hat' 'Ubuntu' 'Suse' 'Fedora' 'UTS' 'OpenLinux');  
pos=3  
Unix=(${Unix[@]:0:$pos} ${Unix[@]:$(($pos + 1))})  
echo ${Unix[@]}  
> Debian Red hat Ubuntu Fedora UTS OpenLinux  

#### 11. Remove Bash Array Elements using Patterns  
declare -a Unix=('Debian' 'Red hat' 'Ubuntu' 'Suse' 'Fedora');  
declare -a patter=( ${Unix[@]/Red*/} )  
echo ${patter[@]}  
> Debian Ubuntu Suse Fedora  

#### 12. Copying an Array  
Unix=('Debian' 'Red hat' 'Ubuntu' 'Suse' 'Fedora' 'UTS' 'OpenLinux');  
Linux=("${Unix[@]}")  

#### 13. Concatenation of two Bash Arrays  
Unix=('Debian' 'Red hat' 'Ubuntu' 'Suse' 'Fedora' 'UTS' 'OpenLinux');  
Shell=('bash' 'csh' 'jsh' 'rsh' 'ksh' 'rc' 'tcsh');  
UnixShell=("${Unix[@]}" "${Shell[@]}")  

#### 14. Deleting an Entire Array  
UnixShell=("${Unix[@]}" "${Shell[@]}")  
unset UnixShell  
echo ${#UnixShell[@]}  
> 0

#### 15. Load Content of a File into an Array  
```
filecontent=( `cat "logfile" `)  
for t in "${filecontent[@]}"  
do  
  echo $t  
done  
```
