<!-- permalink: db7653e595f6dac5b44cd3af2fb218a6 DO NOT DELETE OR EDIT THIS LINE -->
# Atom CTRL-Tab Fix

This fixes the idiotic default behavior for ctrl-tab that Atom ships with for some god-forsaken reason:

Insert this into your keymap

	'body':
		'ctrl-tab': 'pane:show-next-item'
		'ctrl-tab ^ctrl': 'unset!'
		'ctrl-shift-tab': 'pane:show-previous-item'
		'ctrl-shift-tab ^ctrl': 'unset!'

And test it with ctrl-tab.
