---
layout: post
title:      "Transferring a Droplet on DigitalOcean"
date:       2021-05-23 01:55:36 +0000
permalink:  transferring_a_droplet_on_digitalocean
---

I recently acquired a website for my portfolio that was being hosted as a DigitalOcean Droplet. Droplets are like virtual machines in the DigitalOcean world. However, when transferring a website in an acquisition there are a few kinks that can trip you up when dealing with Droplets.

### You Can't Just Transfer a Droplet

Transferring a DigitalOcean Droplet isn't as simple as a domain transfer (although you do need to complete the domain transfer before dealing with anything further in this article). DigitalOcean requires that you take a Snapshot of the Droplet prior to transferring. This is essentially a disk image (remember a Droplet is like a virtual machine) that gets transferred to the new user. 

When logged into your control panel, you can click on "Images" and you should see a menu that says "Take a Snapshot." You can choose your Droplet and enter an image name. Your new Snapshot will appear in the menu below and when you click on the "More" dropdown in the appropriate row, it will give you an option to "Change Owner." After putting in the new owner's information you can choose "Transfer Snapshot" and it will appear in the new owner's account.

### Receiving the Transferred Droplet

The new owner will login to their DigitalOcean account and navigate to Images > Snapshots where a "Pending Transfer" section shows the transferred Snapshot. The new user will select More > Accept and the Snapshot now appears in the new owner's Snapshots menu. From there, select More > Create Droplet and select the options for the new Droplet. 

### Changing the DNS

The new website is now living within a Droplet. Now you need to point the domain to the Droplet. In the DigitalOcean dashboard, select Create > Domains/DNS. You can then add your domain in the "Add a domain" field. The nameservers should be defaulted to DigitalOcean's (ns1, ns2, and ns3) nameservers. Add two A records in the "Create new record" area. You'll want to make sure your two A records are ```www.yourdomainname.com``` and ```yourdomainname.com```. Point these records to your Droplet's IP address (this can be found in your specific Droplet detail page. From there, change your domain's DNS settings on your registrar's page to point to the DigitalOcean nameserves. Wait for the DNS records to propogate (this could take awhile). In the meantime, secure your new web app.

### Securing Your New Web App

In my specific situation, I acquired a web app running a PostgreSQL database. In order to make sure the previous owner has no lingering access ability, you need to make sure their permissions are removed. To do this, you go to your DigitalOcean dashboard and select Droplets, and then your relevant Droplet. The main menu will have a "Console" option which will pull up a virtual console. You can also access this via PuTTY.

The DigitalOcean console is a little weird in that it may just appear as a black screen until you click into it and press a key on your keyboard. From there, you should be able to login using your credentials related to your Droplet and ```cd``` to the directory your files live in. Since Droplets are just virtual machines, you should make sure you get this information from the person you bought the site from in case they have the site files in an uncommon directory. In my situation, the files were in the ```home``` directory.

From there, you'll wanto change the ```postgres``` user's password since they essentially operate as the ```root``` user. So type ```sudo passwd postgres``` and type in a new password. (Note: Since this is a new Droplet, I don't think the previous owner could gain access, but better safe than sorry.) Now log in to postgres by ```sudo -u postgres psql```, change the admin password by typing ```\password postgres``` type in a new password and exit ```psql``` by typing ```\q```.  Log back in to make sure the new password is active.

After you're logged back in, create a new user for yourself by typing ```CREATE USER <username>``` where ```<username>``` is your selected username. Then grant privleges to the newly created user by typing ```GRANT ALL PRIVLEGES ON DATABASE <database> TO <username>``` where ```<database>``` is the database for the new web app and ```<user>``` is the newly created user. From there, drop the previous owner's database user simply by typing ```DROPUSER <username>``` where ```<username>``` is the previous site owner's username (if they had one). You can use the ```\du``` command in the postgres shell to see all users.

From there, make sure the web apps environment variables are accurate as they relate to all the database changes that were just made. Failure to do so, may result in a broken app.

### Conclusion

Buying an already existing web app can be exciting, but with so many hosting options it's important to make sure you fully understand what will be required in order to securely transfer the site before the seller disappears and can no longer offer help.


