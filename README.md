# usercolleting
#script for collectiong User Account 
#code seems to be attempting to collect user account data and display it along with Windows password policy.
#code orginial from book python for security Howard E Poston II  ( Pub : Willey) 

import os
import wmi

w = wmi.WMI()

# Getting list of administrators
admins = None
for group in w.Win32_Group():
    if group.Name == "Administrators":
        users = group.associators(Wmi_result_class="Win32_UserAccount")
        admins = {a.Name for a in users}
        # List user accounts on device
        for user in w.Win32_UserAccount():
            print("Username: %s" % user.Name)
            print("Administrator: %s" % (user.Name in admins))
            print("Disabled: %s" % user.Disabled)
            print("Domain: %s" % user.Domain)
            print("Local: %s" % user.LocalAccount)
            print("Password Changeable: %s" % user.PasswordChangeable)
            print("Password Expires: %s" % user.PasswordExpires)
            print("Password Required: %s" % user.PasswordRequired)
            print("\n")
        # Print Windows password policy
        print("Password Policy:")
        os.system("net accounts")
