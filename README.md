# HestiaCP: Add Multiple NodeJS Apps with QuickApp Installer

You can add multiple websites to your HestiaCP using different ports for each one.

When you create the app with the installer, it automatically creates:
* **/home/%USER%/%DOMAIN%/private/nodeapp** directory
* Config for **nginx** to use the selected port
* **ecosystem.config.js** with the necessary command to connect **pm2** and run your app (e.g., `npm run start`)
* **.nvmrc** file with the node version if you use NVM

---

## How to Install

1. Install Node: (Using one of these options)
   *  [NodeJS](https://github.com/nodesource/distributions)
   *  [NVM](https://github.com/nvm-sh/nvm#installing-and-updating)
2. Install [PM2](https://pm2.keymetrics.io/)
3. Clone this repository:
	```bash
	cd ~/tmp
	git clone https://github.com/dawgcodes/hestiacp-nodejs.git
	cd hestiacp-nodejs
	```

4. Use **install.sh**:
	```bash
	sudo chmod 755 install.sh
	sudo ./install.sh
	```

5. 🚀 You are ready to install an App!!!

---

## How to Use

1. Create a new **user** (If you already have one, no need to create a new one).
2. The user needs bash access for the app to work. Go to **User edit** > **Advanced Options** > **SSH Access** > **bash**.
3. **Add** a new web (e.g., `acme.com`).
4. Go to **Edit** for this new web and select **Quick Install App**.
5. Select **NodeJS** and configure the following:
   * **Node Version**: If you manage Node with NVM, a `.nvmrc` file is placed in the root of the node app with the selected version. If you installed Node without NVM, you can remove this file.
   * **Start Script**: This creates an `ecosystem.config.js` file in the root of the node app with the script you fill in (it should be the one you have in your `package.json`) so PM2 can manage the app.
   * **Port**: You can manage multiple apps with different ports. Assign a different port for each app you have (e.g., 3000). A `.env` file is created in the root of the node app with the selected port. If your app doesn't use this `.env` file, you can remove it.
   * **PHP Version**: This field is only for HestiaCP and can be set to any value (**NOT IMPORTANT**).
6. Go to **Edit Web** > **Advanced Options** > **Proxy Template** > **NodeJS**.
7. Upload your app via the file manager or clone it with Git into `/home/<user>/<domain.com>/private/nodeapp`.
8. 🎉 Congratulations, you're done!!!

---

## FAQ

### How to change the port if I have a web running

First, change the proxy template to **default**, reconfigure the app using the QuickInstall, and finally change the proxy template to **NodeJS**.

### I want to remove the domain

Remove it normally. Open the file manager and delete the folder `hestiacp_nodejs_config/web/<domain.com>`.
