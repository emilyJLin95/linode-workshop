# linode-workshop

# SSH Into Account

ssh root@<your IP address> 

First we need to add a user.
It will ask you to enter a password and ask for some basic user information.
You can just use the default values for the user information.

screenshot of the user creation part

adduser <username> 

To make sure that our user has been created correclty lets switch into that account. su stands for "switch user"

su <username> 

Try running the 

ls 

command.

Our user can't really do anything because he doesn't have any permissions. Lets fix that.

We need to make our user a super user. A super user has many of the same priviledges as the root. Lets switch back to root to do this.

su root

usermod -aG sudo <username> 

Alright, now that our user has super user priviledges lets disable people from logging into root.
Why? Security reasons

A super user can basically do the same thing the root can do.

However, when it comes to attacks, it is easy for attackers to try and login and gain root access because they know the username of root. Its root.
Furthermore, super users have a greater amount of activity logging than root does. So if someone messes something up on the server using a sudo command, we know. 

vi /etc/ssh/sshd_config

scrrenshot of the file

This is using a text editor called VIM. Its a bit wonky to use. Use the arrow keys to move your cursor to where it says 
"#Authentication" 
and find the line that says "PermitRootLogin"
Hit "i" on your keyboard to enter "insert mode" and change "yes" to "no"
Then hit "esc" and then ":" and finally "x" and enter

Now that root login is disabled and you're back on the command line hit "control" + "d" to get yourself out of the ssh.

Try 

ssh root@<your IP address> 

You should not be able to login now.

Lets login with your created account now.

ssh <username>@<Your IP address> 


Now our server is all configured. 
Lets install ngninx!
Ngninx is a webserver that will allow people to enter your IP address in their address bar and see your hosted content!

We're going to be using the apt package manager for this. apt is a package manager, much like how we use npm to manage our packages. 

sudo apt-get update

sudo apt-get install nginx

Ngninx comes with a firewall. We need to reconfigure this to allow us to handle requests. 
Upon installation, Nginx is really kind and configures itself with the firewall "ufw." This means that all we have to do is specify what we want to give Nginx access to. 

Lets list all the possible applications our firewall can work with 

sudo ufw app list

screen shot of this command being run

Nginx Full: allows normal unencrypted web traffic and encrypted traffic
Nginx HTTP: Allows only normal unencrypted web traffic
Nginx HTTPS: Allows only encrypted web traffic

So lets only allow normal web traffic

sudo ufw allow 'Nginx HTTP'

Nginx starts itself after its installed. So it should be running already.

We can double check

systemctl status nginx

scrren shot of this command output


Sweet.
Now we can go to our website hosted website and see whats up.
In our address bar lets put the IP address.
screenshot of the website

Nice! Now lets change it up a bit. 
Go back into terminal and mess with the html
The html can be found at 
/var/www/html/index.nginx-debain.html

