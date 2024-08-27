# Node-RED (dashboard V2)** installation & user guide

*Document version : V1*

[![en](https://img.shields.io/badge/lang-fr-red.svg)](https://github.com/PlanktoScope/node-red-gui-refonte/tree/feat/doc/README.md)

## **Summary**

- *Introduction*
- *Requirements*
- *Installation on PlanktoScope*
- *Using project mode* *Quick dashboard
- *Quick use of the Node-RED dashboard* *Preferences

## **Introduction**

Node-RED is a visual development tool for connecting hardware devices, APIs and online services in new and exciting ways. It offers an intuitive interface for building application flows by connecting nodes that represent distinct blocks of functionality. In this documentation, we'll guide you through the process of installing, configuring and using Node-RED, particularly in the context of PlanktoScope.

## **Prerequisites**

**PlanktoScope**: Make sure PlanktoScope is correctly installed and accessible via SSH.  
**GitHub account**: A GitHub account is required to manage projects and access tokens.  
**SSH access**: You must be able to connect to your PlanktoScope via SSH to modify Node-RED configuration files.


## **Installation on the PlanktoScope**.

1. **Accessing the PlanktoScope V1 Dashboard** (in French)

After inserting an SD card containing the PlanktoScope image, the V1 dashboard is available online. You can access the PlanktoScope landing page at the following address:

**Landing page :** `http://<planktoscope-ip-address>`

From this page, several options are available, including :

* **Node-RED dashboard editor :** This link gives you access to the dashboard editor. This editor allows you to modify and customize the various elements of the dashboard.

* **Node-RED dashboard:** This link takes you to the V1 version of the dashboard. However, please note that once you have installed version V2, this link will no longer work.


2. **Starting PlanktoScope** : Start by opening a terminal on your local machine.

**Open a terminal**: Start by opening a terminal on your local machine.  
**SSH connection**: Connect to PlanktoScope via SSH using the following command:

```
ssh pi@<planktoscope-ip-address>
```

Replace \<planktoscope-ip-address> with the IP address of your PlanktoScope.  
Then enter the password in the command prompt, which should look like this:

```
Please note that SSH may not work until a valid user has been set up.

See http://rptl.io/newuser for details.
pi@92.167.184.163's password:<password>
```

Replace <password> with “copepode”.

3. **Node-RED** configuration  

3.1 **Edit settings.js** file

To configure Node-RED, you need to edit the settings.js configuration file.

A. **File location** : The settings.js file is located in the /etc/nodered/ directory, and can be accessed with the following command: 

```
cd /etc/nodered/
```

Open the file with a text editor *(example “nano” or “vim”)*.

B. **Modifying parameters** :  
   * **Enable context storage (contextStorage)**: Remove comments to enable contextStorage. This saves data between Node-RED reboots.  
   * Project mode**: Change the value from enabled to true to activate project mode. This will enable you to manage your feeds with version control via Git.

Example of modification in settings.js for contextStorage :

```javascript
// Remove comments to activate the next part
contextStorage: {
    default: {
        module: "localfilesystem"
    }
},
```

### Example of modification in settings.js for project mode : 

```javascript
// Set the value of the “enable” attribute to true in the following section
editorTheme: {
    projects: {
        enabled: true
    }
}
```

Once you've made your changes, on “nano” you need to press “ctrl+x” then “y” and the “enter” key to exit while saving.

3.2 **Restarting Node-RED** (in French)

After modifying the configuration file, restart Node-RED to apply the changes:

```
sudo systemctl restart nodered
```

Once Node-RED has been restarted, open the editing interface via a web browser by logging in via the link on the landing page:

- **Node-RED dashboard editor**

4. ## **Node-RED use**

   4.1 **Editing interface**

After starting Node-RED, you'll be greeted by the editing interface, where you can create and manage your feeds. With project mode activated, you can now manage your projects. 

<p align="center">
    <img src="image-doc/Screen-1.png" alt="Screen 1" width="30%"/>
    <img src="image-doc/Screen-2.png" alt="Screen 2" width="30%"/>
</p>

**Screen 1 :** To retrieve Dashboard V2, please click on Clone repository. 

**Screen 2 :** Please fill in Username and Email with the ones you want *(e.g. Put in your current Github credentials)*. This information will be used to identify you during push/pull operations. Then click on Next.

<div style="display: flex">
    <p align="center">
        <img src="image-doc/Screen-3.png" alt="Screen 3" width="70%"/>
    </p>
    <p align="center">
        <img src="image-doc/Screen-4.png" alt="Screen 4" width="55%"/>
        <img src="image-doc/Screen-5.png" alt="Screen 5" width="55%"/>
    </p>
</div>

**Screen 3:** Here you'll need to retrieve the .git link for the repository you wish to clone. In our case the link is: https://github.com/PlanktoScope/node-red-gui-refonte.git  
Copying and pasting this link into the Git repository URL text box will automatically retrieve the Project name. Now fill in Username and Password with your Github credentials, then click on Clone project.

**Screen 4 & 5 :** If you get this warning about credentials, please click Setup credentials. Then click on edit and on the pencil, then enter a new key to be used for encryption *(ex: plk\_q8dSMZ7HIPyi8o7LSDJudWvd2B3Ro)* then click on Save and Close. 

<div style="display: flex">
    <p align="center">
        <img src="image-doc/Screen-6.png" alt="Screen 6" width="45%"/>
        <img src="image-doc/Screen-7.png" alt="Screen 7" width="45%"/>
        <img src="image-doc/Screen-8.png" alt="Screen 8" width="45%"/>
        <img src="image-doc/Screen-9.png" alt="Screen 9" width="45%"/>
    </p>
</div>

**Screen 6 :** Click on the gray icon.

**Screen 7 & 8 & 9 :** After modifying credentials, you'll see the node-RED files that have been modified in Local files. Just click on \+all to add and select the files. Then in **Screen 8** click on commit, a text box will appear. In it, write a description of what's been modified, a short explanation of what you've done (in our case, it might be update/credentials), then click on Commit. Now click on Commit History, which will open a tab showing your last commit and a button with two arrows, click on it, then on push.

<img src="image-doc/Screen-10.png" alt="Screen 10" width="45%"/>

**Screen 10:** Once step **screen 9** is complete, this pop-up asks you to enter your Github login details. Here, your Password is actually an access-token that you'll need to generate from Github. I refer you to the [documentation](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens\#creating-a-personal-access-token-classic) link, and once you've retrieved it and entered Password, click Retry.

Once all these steps have been completed, you'll need to restart node-RED as you did in step **3.2 Restart Node-RED**.

<div style="display: flex">
    <p align="center">
        <img src="image-doc/Screen-11.png" alt="Screen 11" width="45%"/>
        <img src="image-doc/Screen-12.png" alt="Screen 12" width="45%"/>
    </p>
</div>

**Screen 11:** Once the dashboard has been reopened, node-RED tells you that there are some missing dependencies. Just go to Manage project dependencies.

**Screen 12:** Here you can see the two dependencies that node-RED offers. Just click on install, then Close, then refresh the web page.

<div style="display: flex">
    <p align="center">
        <img src="image-doc/Screen-13.png" alt="Screen 13" width="45%"/>
        <img src="image-doc/Screen-14.png" alt="Screen 14" width="45%"/>
    </p>
</div>

**Screen 13:** You should have one dependency left: downloadfile. Then click on Manage project dependencies.

**Screen 14:** Here you have the complete list of dependencies. You'll need to delete any that are no longer in use. In our case : 
- node-red-contrib-dir2files,  
- node-red-contrib-gpsd,  
- node-red-contrib-python3-function,  
- node-red-contrib-ui-multistate-switch,  
- node-red-dashboard,  
- node-red-node-pi-gpio,  
- node-red-node-ui-list

Then go to the Install tab, search for and install the downloadfile module *(@prescient-devices/node-red-contrib-downloadfile).* Once installed, you'll need to refresh the page and your online V2 installation with github project is complete.