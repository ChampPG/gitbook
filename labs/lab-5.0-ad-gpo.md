# Lab 5.0: AD GPO

### Summary

This lab seemed very straight forward but I was never able to figure out the 1612 error I was getting. It didn't matter what permissions I gave the file share it would continue to do this. I almost wish we had used a program like sccm because I use that on a daily basis and I am able to understand permissions there. Overall the rest of this lab went well I wish I was able to actually complete it though.

### Powershell

#### Creating an OU

* `New-ADOrganizationalUnit “<Name>” –Path “DC=paul,DC=local”`

#### Delete an OU

* `Get-ADOrganizationalUnit -filter "Name -eq '<Name>'" | Set-ADOrganizationalUnit -ProtectedFromAccidentalDeletion $False`
* `Get-ADOrganizationalUnit -filter "Name -eq 'Continents'" | Remove-ADOrganizationalUnit –Recursive`

I had no problems but I know people had an issue with the accidental deletion variable.

#### Get event in Powershell

* `Get-WinEvent -FilterHashTable @{loginame='System'; id=<Id>} -MaxEvents 1` This will list 1 event with the ID from the System tab
