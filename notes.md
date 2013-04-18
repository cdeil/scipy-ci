# Developer notes

* Machine is at URL d3-4.macminivault.com 
* ci.scipy.org forwards there
* If you go there in your web browser, you can see the Jenkins dashboard.

# Admin notes

* To create a new user, run the `create_user_account.sh` script with sudo.
* To give a user admin permissions use `sudo dscl . append /Groups/admin GroupMembership username`
