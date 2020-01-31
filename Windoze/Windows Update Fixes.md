<!-- permalink: bdcee8d7c7517b9fc086f2846f2367e3 DO NOT DELETE OR EDIT THIS LINE -->
# Windows Update Fixes

### Fix A

1. Open a *Command Prompt* (Run as Administrator).
1. `cd %windir%`
1. `net stop wuauserv`
1. `ren softewaredistribution softwaredistribution.old`
1. `net start wuauserv`
1. Try installing the updates once again.
