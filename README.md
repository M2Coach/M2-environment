# Requirements

1. VirtualBox 5.2 or higher
2. Vagrant 2.0 or higher
3. Vagrant `disksize` plugin: (install: `vagrant plugin install vagrant-disksize`)

* Set values `magento2_auth_public_key` and `magento2_auth_private_key` in `./ansible/group_vars/all/main.yml` file. These credentials are necessary to set up the Magento 2 composer install https://devdocs.magento.com/guides/v2.2/install-gde/prereq/connect-auth.html


# Setup

1. Inside `./environment/` directory execute `vagrant up`. In your VirtualBox GUI new box should be created `environment_default_abcdefghijklmnoqprstuw`
2. Log in using SSH to new virtual machine (`vagrant ssh`), get the latest external roles with `ansible-galaxy install -r roles.yml -p roles/`.
3. Change current user to `deployer`, using `sudo su deployer`. Enter `/ansible/` directory. Run `ansible-playbook provision-system.yml -i development.ini`. Execution installs all the necessary dependencies to run the Magento and Magento itself.
3. Add new host binding to `hosts` file

   Windows: Run `Notepad` as administrator, open `c:\Windows\System32\Drivers\etc\hosts`
   Linux: Open `/etc/hosts` in your favorite text editor in sudo mode

   then add extra line to the file
   ```
   172.16.55.100  m2coach.magento.local
   ```

4. Mount network resource using NFS:
   * Linux: `$ sudo mount m2coach.magento.local:/var/www/m2coach/ ./project/`
   * Mac: `$ sudo mount -o revsport m2coach.magento.local:/var/www/m2coach/ ./project/`
   * Windows: Open `Programs and Features`, look for `Services for NFS`, then select `Client for NFS`. Press `Close`. You can run commandline now (`cmd`) and run `mount -o anon m2coach.magento.local:/var/www/m2coach Z:`. In your "Computer", new drive should be available as `Z:` drive
