<!-- permalink: 4da2294b935edc055ab44f9636b84efd DO NOT DELETE OR EDIT THIS LINE -->
# Windows Time Synchronization

Before anything will work, you need to be sure that the computer functioning as the time server allows connections on port 123 both on the server itself and through any firewalls between the clients and the server.
	* For Windows firewall settings reference, this is the path to allow connections to: `%SystemRoot%\System32\w32tm.exe`


# BEFORE STARTING READ THIS

**Don't change the clock by more than 10 minutes at a time!** Doing so can cause AD or group policy or something super important to break!


The following is all to setup clients to sync with the server:

1. Run `w32tm /query /source` to see what the current time source is.
2. If it needs to be changed, run `w32tm /config /manualpeerlist:*timeservers* /syncfromflags:manual /reliable:yes /update`
	* to set more than one server, follow this example: `w32tm /config /manualpeerlist:"timeserver1.domain or.activedirectory.server" /syncfromflags:manual /reliable:yes /update`
	* you can also use internet time servers like `w32tm /config /manualpeerlist:"0.pool.ntp.org, 1.pool.ntp.org, 2.pool.ntp.org" /syncfromflags:manual /reliable:yes /update`
3. If the client is a VM, make sure that the time syncing service is off. This has to be set in the HyperV host settings for the VM.
4. Run `net stop w32time && net start w32time` to restart the time service
	* This may or may not be necessary, but it can jump start the process at the very least
5. The settings don't take hold immediately. In fact, running `w32tm /query /source` will most likely reutrn `Local CMOS something or other`. Give it a minute and try again, and it should say the correct source.
6. gg


### Other useful commands and resources

* `w32tm /query /peers`
	* returns a list of "peers" to source time information from
* `w32tm /monitor`
	* prints the connection status to sources
* `w32tm /query /configuration`
	* prints the entire configuration
* `reg query HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameter`
	* checks the actual registry setting
* [reference](https://blogs.msdn.microsoft.com/virtual_pc_guy/2010/11/19/time-synchronization-in-hyper-v/)
