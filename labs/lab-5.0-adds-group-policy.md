# Lab 5.0: ADDS Group Policy

### Summary

This lab was very straight forward except I hit a roadblock when it came to the `disablelastlogin`. Overall it was a very fun lab and I hope I do well when everything is deleted.

### Assessment Prep

Remember to enable ICMP on windows and follow my documentation.

### Commands / Steps

1. To add an Organization Unit or OU
   * Go to `tools` then select `Active Directory Users and Computers`
   * Right-click on name.local `new` then `Organizational Unit`
   * Now create `Accounts`, `Computers`, `Groups`
2. To add users to the OU
   * Right-click on the Accounts `New` then `User`
3. To add a computer to an OU
   * Do the same as before except select `Computer` instead of `User`
4. Creating Group Policy for OU
   * Select your `Groups` then right-click on the Accounts `New` then `Group`
   * Here you want to add the users to that policy
5. Group Policy Management
   * Go to `tools` then select `Group Policy Management`
   * Select the OU created before and `Create a GPO in this domain, and Link it here...`
   * Now remove `Authenticated Users` and add the name of the Group Policy created before
   * Next add the `Domain Computers` so this affects all computers in the Domain
   * Next got to `Delegations` tab and to `Domain Computers` and change the Permissions so Deny is checked for `Apply Group Policy`

To Clear Login After Every Logout \* Create `DisableLastLogin` under the `Computers` OU \* Now remove `Authenticated Users` and add the name of the Group Policy created before \* Next add the `Domain Computers` so this affects all computers in the Domain \* Make sure `Apply Group Policy` is checked under the `Delegation` tab for `Domain Computers` \* Now right click on `DisableLastLogin` and select edit `Computer Config/Policies/Windows Settings/Security Settings/Local Policies/Security Options` right click on `Security Options` then find `Don't display last signed-in` and enable

PLEASE HIT APPLY WHEN YOU WANT TO CHANGE POLICY

1. To edit this new GPO
   * Right-click and select `Edit`
   * Now if you want to remove the recyling bin navigate to `User Configuration/Administrative Temp/Desktop` and under desktop will be everything that can be changed
2. To check if GPO is applied
   * On a domain computer and login then pull up a power shell and type `gpresult /r`
     * under `Applied Group Policy Objects` will show what rules are applied
     * `gpudate /force` = will update the group policy by force
   * `gpresult /scope computer /r` = shows what is applied to current computer
