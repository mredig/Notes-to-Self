<!-- permalink: ea574d6597dd4d0ae0c7769f112a2b48 DO NOT DELETE OR EDIT THIS LINE -->
# Windows Group Policy Administrative Template Setup


## Create a Central Store
The central store is a folder structure created in the sysvol directory on the domain controllers in each domain in your organization. You will need to create the central store only once on a single domain controller for each domain in your organization. The File Replication service then replicates the central store to all domain controllers. It is recommended that you create the central store on the primary domain controller because the Group Policy Management Console and Group Policy Object Editor connect to the primary domain controller by default.
The central store consists of a root-level folder containing all language-neutral ADMX files and subfolders containing the language-specific ADMX resource files.
To perform this procedure, you must be a member of the Domain Admininstrators group in Active Directory.
### To create the central store
1. Create the root folder for the central store %systemroot%\sysvol\domain\policies\PolicyDefinitions on your domain controller.
1. Create a subfolder of %systemroot%\sysvol\domain\policies\PolicyDefinitions for each language your Group Policy administrators will use.
	* Note: Each subfolder is named after the appropriate ISO-style Language/Culture Name. For a list of ISO-style Language/Culture Names, see Valid Locale Identifiers. For example, to create a subfolder for U.S. English, create the subfolder: %systemroot%\sysvol\domain\policies\PolicyDefinitions\EN-US

## Populate the Central Store with ADMX Files
There is no user interface for populating the central store in Windows Vista. The procedure shows how to populate the central store using command line syntax from the Domain Controller.
### To populate the central store
1. Open a command window: click Start, click Run, then type cmd.
1. To copy all the language-neutral ADMX files from your Windows Vista administrative workstation to the central store on your domain controller using the xcopy command, type:
	* `xcopy %systemroot%\PolicyDefinitions\* %logonserver%\sysvol\%userdnsdomain%\policies\PolicyDefinitions\`
1. To copy all ADMX language resource files from your Windows Vista administrative workstation to the central store on your domain controller using the xcopy command, type:
	* `xcopy %systemroot%\PolicyDefinitions\EN-US\* %logonserver%\sysvol\%userdnsdomain%\policies\PolicyDefinitions\EN-US\`


## Edit the Administrative Template Policy Settings in the Domain-Based GPOs
You can edit GPOs only using ADMX files on a Windows Vista-based computer.
### To edit administrative template policy settings using ADMX files
1. To open the Group Policy Management Console on a Windows Vista machine, click Start, click Run, then type GPMC.msc.
1. To create a new GPO to edit, right-click the Group Policy objects node and select New.
1. Type a name for the GPO and click OK.
1. Expand the Group Policy objects node.
1. Right-click the name of the GPO you created and click Edit.
1. The Group Policy Object Editor automatically reads all ADMX files stored in the central store. When there is no central store, the Group Policy Object Editor reads the local versions of the ADMX files used by the local GPO on your Windows Vista administrative machine.
* Note   You can still remove and add ADM files to the GPO. There is no user interface for adding or removing ADMX files in Windows Vista.
To add local ADMX files to the Group Policy editing session, copy the ADMX files to the `%systemroot%\PolicyDefinitions\` folder and restart the Group Policy Object Editor.


[reference](https://msdn.microsoft.com/en-us/library/bb530196.aspx)
