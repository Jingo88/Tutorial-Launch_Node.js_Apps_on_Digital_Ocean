# Launching a Node.js Website on Digital Ocean

##### [I. Creating a Droplet](#create)
##### [II. Adding Your Domain Name](#dns)
##### [III. Adding "www" to Your URL](#www)
##### [IV. Pull a Git Repo](#pull)
##### [III. Starting and Stopping Your Site](#start)


#### <a name=create>Creating a Droplet</a>

* Log into your Digital Ocean account and click on "Droplets"
* Click "Create Droplet" the green button on the top
* Name your Droplet and choose from a select size. 
* You don't need to check of anything in Available Settings
* Select Ubuntu
* Do not add SSH keys


#### <a name=dns>DNS - Adding your domain name</a>

* Go to the DNS tab
* If you bought a domain you can add it under the "Add a Domain" section
* Select your newly created droplet from the drop down menu
* Click "Create Domain"
* Depending on where you bought your domain from you need to go to that original site
* Change your Domain Name Server information to the links next to the "NS" tab on the DNS Digital Ocean page
* Apply these changes and it can take up to 24-48 hours to complete


#### <a name=www>Adding "www" in Front of Your URL</a>

* Go to your domain on the DNS tab of Digital Ocean
* Select "Add Record" - the big ass blue button
* Seclect "CNAME" from the list that appears
* The first box with "Enter Name" please put "www"
* The second box with "Enter Hostname" please put "yourdomain.com"
* This will allow users to go to your site whether they input your domain with or without the "www" in front of it

#### <a name=pull>Pull a Git Tepo</a>

* SSH into your Digital Ocean server. The command should look something like

```
ssh root@yourdomainname.com
```

* You are now the root user and in the "home" section of the "root" folder
* You need to only run this command once. It will pull from a repo the Ubuntu installation

```
bash <(wget -qO- http://gitlab.generalassemb.ly/princess-peach/install_fest/raw/master/install_script_ubuntu)
```

* Now create a directory and connect the repo you plan to pull from

```
git init
git remote add origin HTTPSlinkfromrepo
git pull origin master
```

#### <a name=start>Starting and Stopping Your Site</a>

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

**Pull and update Git files**













