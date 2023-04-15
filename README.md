# linux cheatsheet
## Linux Basic Command
<br/>1.ls		 {Lists all files and directories in the present working directory}
<br/>2.ls -R 	{Lists files in sub-directories as well}
<br/>3.ls -a		{Lists hidden files as well}
<br/>4.ls -al		{Lists files and directories with detailed information like permissions,size, owner, etc.}
<br/>5.cd or cd 	{	Navigate to HOME directory}
<br/>6.cd ..			{Move one level up}
<br/>7.cd	 	{To change to a particular directory}
<br/> cd /folder/folder/folder {direct path}
<br/>8.cd /	 	{Move to the root directory}
<br/>9.cat > filename		{ Creates a new file}
<br/>10.cat filename		{Displays the file content}
<br/>11.cat file1 file2 > file3		{Joins two files (file1, file2) and stores the output in a new file (file3)}
<br/>12.mv file "new file path"		{Moves the files to the new location}
<br/>13.mv filename new_file_name		{Renames the file to a new filename}
<br/>14.pwd 	{Show current directory}
<br/>15.rm filename		{Deletes a file}
<br/>16.history		{Gives a list of all past commands typed in the current terminal session}
<br/>17.clear		{Clears the terminal}
<br/>18.rmdir		{Deletes a directory}
<br/>19.mv		{Renames a directory}
<br/>20.pr -x		{Divides the file into x columns}
<br/>21.pr -h		{Assigns a header to the file}
<br/>22.apt-get 	{Command used to install and update packages}
<br/>
## File Permission
<br/>1.ls -l		{to show file type and access permission}
<br/>2. r		{read permission}
<br/>3.w 		{write permission}
<br/>4.x 		{execute permission}
<br/>5. Chown user		{For changing the ownership of a file/directory}
<br/>6. chmod u+x file_name {add execute permissions for the owner}
<br/>7. chmod g+rw file_name{dd read and write permissions for the group }
# Apache for static web
### uninstall Apache2
<br/>sudo service apache2 stop
<br/>sudo apt-get remove apache2
<br/>sudo apt-get purge apache2
<br/>sudo apt-get autoremove
<br/>sudo rm -rf /etc/apache2
## install apache2
</br>apt-get install httpd -y
<br/>sudo apt-get install apache2
<br/>apache2 -version
### SSH Connection
<br/>ssh -i nibir.pem username(ubuntu)@3.86.200.159
<br/>sudo su
<br/>sudo apt-get update
<br/>systemctl status apache2
<br/>cd var/www/html/
<br/> use nano for edit index.html
<br/>
<br/>
<br/>
<br/>
<br/>
<br/>


