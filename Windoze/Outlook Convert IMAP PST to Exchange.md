<!-- permalink: d89fbf1e00a71c380045ca027eb5d8ce DO NOT DELETE OR EDIT THIS LINE -->
# Outlook Convert IMAP PST to Exchange

1. Open pst in Outlook - note the profile you're using it in. (this won't work on a non cached pst)
1. Close Outlook and open [MFCMAPI](https://mfcmapi.codeplex.com/)
	* Apparently google is warning that this link is unsafe and hosting malware - I don't believe that was the case upon initial writing, but reader beware...
1. Use the menu option *Session -> Logon* and select the profile from earlier
1. Open the data file needing conversion from the list
1. Go through all folders looking at the *PR_CONTAINER_CLASS* property. If there are any with the value *IPF.Imap* change it to `IPF.Note`
1. Close the window, log out of the same session menu, and close *MFCMAPI*
1. Open Outlook and confirm it's working
