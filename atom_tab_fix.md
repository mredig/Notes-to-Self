# Atom CTRL-Tab Fix

This fixes the idiotic default behavior for ctrl-tab that Atom ships with for some god-forsaken reason:

Insert this into your keymap

	'body':
		'ctrl-tab': 'pane:show-next-item'
		'ctrl-tab ^ctrl': 'unset!'
		'ctrl-shift-tab': 'pane:show-previous-item'
		'ctrl-shift-tab ^ctrl': 'unset!'

And test it with ctrl-tab.
