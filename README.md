# Wordpress Starter Kit - Date 28 june, 2019

# This starter kit includes
1. https://github.com/louim/bedrock-site-protect
2. https://www.typist.tech/projects/trellis-cloudflare-origin-ca
3. https://github.com/valentinocossar/trellis-database-uploads-migration
4. https://github.com/ItinerisLtd/trellis-backup-during-deploy
5. https://github.com/ItinerisLtd/trellis-cve-2018-6389
6. https://github.com/ItinerisLtd/trellis-disable-xml-rpc

# This starter kit excludes

## SMTP Settings

So emails in Staging and Production won't go through.

To set up email, you may use elasticemail.com

Setting it up looks like this - 

Link to official documentation: https://roots.io/trellis/docs/mail/

Following settings are set in group_vars/all/mail.yml -

```
mail_smtp_server: smtp.elasticemail.com:587
mail_admin: mail@maaef.com
mail_hostname: maaef.com
mail_user: maaeftech@gmail.com
mail_password: "{{ vault_mail_password }}" # Define this variable in group_vars/all/vault.yml
```

# Instruction to get up and running quickly

1. Copy this starter kit into domainname.com folder
```
git clone git@github.com:amankapoor/trellis-wordpress-starter-kit.git .
```
AND THEN REMOVE .GIT FOLDER - VERY IMPORTANT

2. Create .vault_pass in trellis folder and enter some password

3. Search for 'neticians' and change it to domain name everywhere

4. Use https://www.lastpass.com/password-generator to generate 36 character passwords for vaults

5. Get cloudflare credentials for origin key

6. Replace all generate me

7. Install Galaxy roles: ansible-galaxy install -r requirements.yml (in local trellis directory)

8. Run `composer update` in site directory

9. Run `vagrant up` in trellis directory to run the site locally

10. Add IP addresses in host files for staging and/or production

11. Encrypt all vault files using - 

```
ansible-vault encrypt group_vars/all/vault.yml group_vars/development/vault.yml group_vars/staging/vault.yml group_vars/production/vault.yml
```

12. Provision server using 
```
ansible-playbook server.yml -e env=<environment>
```

13. Deploy using
```
ansible-playbook deploy.yml -e "site=mysite.com env=production"
```

13. Push Database (Docs - https://github.com/valentinocossar/trellis-database-uploads-migration)
```
./bin/database.sh staging neticians.com push
```

14. Push Uploads
```
./bin/uploads.sh staging neticians.com push
```

# Notes:

1. Emails during development can be found at at http://yourdevelopmentdomain.test:8025

2. Keep regularly pushing the project to git repo to keep things updated

3. Use the code `xclip -sel clip < ~/.ssh/id_rsa.pub` to get SSH key for server

