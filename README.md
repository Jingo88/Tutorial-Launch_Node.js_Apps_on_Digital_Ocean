# Connecting to Digital Ocean and Launching a Node.js Website

##### [I. What is Digital Ocean](#intro) 
##### [I. Creating a Droplet](#create)
##### [I. Connecting to the Droplet](#connect)
##### [I. Cloning a Repo](#clone)
##### [III. Starting and Stopping Your Site](#start)
##### [II. Adding Your Domain Name](#dns)
##### [III. Adding "www" to Your URL](#www)

### <a name=intro>What is Digital Ocean / SSH</a>
---

Digital Ocean is a hosting service which allows us to put our code online and launch our web application for the whole world to see. 

So what about these questions?

* What is a server?
* Can a computer be a server?
* Are we able to connect to another computer `remotely`?
* Can we connect to a server `remotely`?

A server is a computer that servers up data. We can access computers remotely so we must be able to access server. That's what we're doing now, building a connection to a server powered by Digital Ocean.

A server is a computer that:

* acts as a central interface for data
* manages interaction between clients / computers

SSH is a UNIX command we use to log into another computer via the terminal over a network. It allows us to execute commands remotely!

### <a name=create>Creating a Droplet</a>
---

* Run the following command to copy your ssh key from your terminal. `pbcopy` will automatically copy the key

```
pbcopy < ~/.ssh/id_rsa.pub  
```
* Log into your Diginal Ocean account > Settings > Security > Add SSH Key
	* You can make the name anything you would like it to be and you can include more than one SSH key
* Log into your Digital Ocean account and click on "Droplets"
* Click "Create Droplet" the green button on the top
* Name your Droplet and choose from a select size. 
* You don't need to check of anything in Available Settings
* Region = USA, unless you're somewhere else? o.O
* Select Ubuntu
* Do not add SSH keys
* Digital Ocean will send you an e-mail with the initial login information

### <a name=connect>Connecting to the Droplet</a>
---

* Look into the email you got from Digital ocean. It will contain a password and IP address.

```
ssh root@YOUR-IP-ADDRESS
```
* Lets run a quick update
* apt-get is a repository that manages the installation of packages for Ubuntu
	* Like what brew does for OSX
	* Like what npm does for node

```
apt-get update
```

* Now install what you need for your app. The below code installs `git` and `node` for us to use. 

```
apt-get install git

apt-get install nodejs

apt-get install nodejs-legacy

apt-get install npm
```

### <a name=clone>Cloning your repo</a>
---

* If you logged out of your droplet, SSH back into your Digital Ocean server. The command should look something like

```
ssh root@yourdomainname.com
```
* You should be in the `home` section of the `root` user. 
* Now create a directory and connect the repo you plan to pull from

```
git init
git remote add origin HTTPSlinkfromrepo
git pull origin master
```

### <a name=start>Starting and Stopping Your Site</a>
---

**Start server regularly** 

```
node server.js -p80
```
* You should be able to go to your domain name or ip address now in a web browser
* The "-p80" prevents the user from having to type ":8080" at the end of the url
* Once you close your terminal your server will stop and your site will not be live


**Start server in the background**

```
nohup node server.js -p80 &
```
* nohup - allows you to continue working in your terminal because it runs the process in the background
* & - this tells your DO box to continue running the process even when your terminal disconnects
* Your site will be live whether your terminal is connected or not, your computer is on or off


**Stop your server**

* If you started your server regularly you could just exit or ctrl+c it
* If you nohup'd your server use the following command to find the process number

```
ps aux | grep server
```

* ps aux - gives the entire command line of the processes which are searched
* grep - will search any process that is running that contains the word you put after it
* You can also run other words after grep such as "nohup," "node," and the like
* Now take the process number for the server that is running and input the following command

```
kill -9 processnumber
```

* Your site is no longer up
* You can also remove your nohup.out log file as well. This was created when you first ran the nohup command

```
rm nohup.out
```
### <a name=dns>DNS - Adding your domain name</a>
---

* Go to the DNS tab
* If you bought a domain you can add it under the "Add a Domain" section
* Select your newly created droplet from the drop down menu
* Click "Create Domain"
* Depending on where you bought your domain from you need to go to that original site
* Change your Domain Name Server information to the links next to the "NS" tab on the DNS Digital Ocean page
* Apply these changes and it can take up to 24-48 hours to complete


### <a name=www>Adding "www" in Front of Your URL</a>
---

* Go to your domain on the DNS tab of Digital Ocean
* Select "Add Record" - the big ass blue button
* Seclect "CNAME" from the list that appears
* The first box with "Enter Name" please put "www"
* The second box with "Enter Hostname" please put "yourdomain.com"
* This will allow users to go to your site whether they input your domain with or without the "www" in front of it

