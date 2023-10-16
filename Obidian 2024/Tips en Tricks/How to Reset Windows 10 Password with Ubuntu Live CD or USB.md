Forgot administrator password of your Windows 10 PC? If you had not [created a Windows 10 password reset disk](https://www.top-password.com/knowledge/create-windows-10-password-reset-disk.html) earlier, then you're left with an option to reinstall Windows, but that will erase all your files and settings. Well, do not worry. In this tutorial we will discuss how to reset Windows 10 password with Ubuntu Live CD or USB drive, when you forgot your computer password.

## How to Reset Windows 10 Password with Ubuntu Live CD/USB

1. To get started, just download Ubuntu Desktop free from [Ubuntu official website](https://www.ubuntu.com/download/desktop) (about 1.4 GB). Burn the ISO image to a CD (or USB flash drive) using the freeware [ISO2Disc](https://www.top-password.com/iso2disc.html).
2. Insert the Ubuntu Live CD into the computer that you want to reset the password for, then you need to boot off the disc. Once booted to the Ubuntu Live welcome screen, choose **Try Ubuntu**.
    
    ![](https://www.top-password.com/images/ubuntu/try-ubuntu.png)
    
3. Open **System Settings** and then click on **Software and Updates**. In the window that appears, check the "**Community-maintained free and open-source software**" option and click **Close**.
    
    ![](https://www.top-password.com/images/ubuntu/software-updates.png)
    
4. A dialog will appear with the repository information is out of date. You have to Click the **Reload** button.
    
    ![](https://www.top-password.com/images/ubuntu/ubuntu-reload-updates.png)
    
5. Open a terminal, then run the following command to install the password resetting utility you'll need.
    
    sudo apt-get install chntpw
    
    ![](https://www.top-password.com/images/ubuntu/install-chntpw-in-ubuntu.jpg)
    
6. Now find your Windows partition and browse to the directory _Windows\System32\Config_. Right-click blank space and select **Open in Terminal**.
    
    ![](https://www.top-password.com/images/ubuntu/windows-config-folder.png)
    
7. In the terminal, run the following command and it will list out all the user accounts that are contained on your Windows 10 system.
    
    chntpw -l SAM
    
    ![](https://www.top-password.com/images/ubuntu/chntpw-list-users.png)
    
8. If you would like to reset lost password for a specific account, type the following command and press Enter.
    
    chntpw -u user_name SAM
    
    ![](https://www.top-password.com/images/ubuntu/chntpw-reset-user-passwor.png)
    
9. You'll be presented with several options to reset the password, unlock / enable / promote user account. Type **1** and press Enter.
    
    ![](https://www.top-password.com/images/ubuntu/clear-user-password-with-chntpw.png)
    
10. Type **q** and hit Enter at this point to quit the User Edit Menu.
    
    ![](https://www.top-password.com/images/ubuntu/quit-editing-user.png)
    
11. Then type **y** to confirm and save the changes.
    
    ![](https://www.top-password.com/images/ubuntu/write-hive-files.png)
    
12. Reboot your computer and take out the Ubuntu Live CD from the disc drive. You can then log into Windows 10 without a password!

This method is easy to follow for Linux users to reset Windows 10 local user password. If you're looking for a much easier yet professional live CD/USB to bypass Windows 10 Microsoft / local password, you can try [PCUnlocker](https://www.top-password.com/reset-windows-password.html).