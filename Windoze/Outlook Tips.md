<!-- permalink: 490f2bb754434c653f12919d74b20d2e DO NOT DELETE OR EDIT THIS LINE -->
# Outlook Tips

### Merge Calendars
1. Set the view to *list* - now you can drag items from one calendar to another.

### Folder View
* On versions 2013 and newer we don't have the whole folder structure exposed to us simpleton users by default. On the row of icons that allow you to navigate between mail, calendar, contacts, and tasks, there's also an ellipses button (...) that you can use to select the traditional folder view.

### Send From Shared Box
1. Set *Send As* permission on exchange
1. Default is to place sent items in the personal users mailbox. If this is what you want or don't care, no need to proceed.
	* example: Zelda and Link both have mailboxes. They also both share a mailbox called TriForce. By default, when Link sends a message from TriForce, it places the sent message in **Link's** sent box, NOT **TriForce's** sent box. (Same goes for Zelda in her sent box)
1. If you want the sent items to goto the shared mailbox, proceed:
1. *Cached Mode* MUST be on! In a terminal environment, you will likely just want to limit it to the minimum time frame.
1. The following registry entry must be set on the client machine (must be set for every computer Link uses, etc) (This is for Outlook 2013, 2016 would use 16.0 I believe is all the difference)

		Windows Registry Editor Version 5.00

		[HKEY_CURRENT_USER\Software\Microsoft\Office\15.0\Outlook\Preferences]
		"DelegateSentItemsStyle"=dword:00000001

1. Close and reopen Outlook - send a test message to confirm. GG
