# theweirdcommandscollection
#### The ultimate collection of "damn I should write that down" commands & fixes

## The Poor Man's nmap
On a windows machine, this line conducts a ping scan similar to nmap on /24 networks:
for /L %z in (1,1,254) do @ping 192.168.0.%z -w 10 -n | find "Reply"

## VMWare Failed to Create VMFS Datastore Test Error
#### Preface:
Full error message will be "Failed to create vmfs datastore test - cannot change the host configuration"
#### Fix:
Step 1. ssh into the host
Step 2. run ls -lha /vmfs/devices/disks/ and get the .vmdk diskID
Step 3. run partedUtil getptbl /vmfs/devices/disks/(diskID) msdos
> Response should be '0 0 0 0'

## VMWare Reformat a .vmdk Created in Workstation for use in ESXi
#### Preface:
.vmdks made in VMWare's Workstation will not run as VMs in ESXi without first being converted
#### Fix:
vmkfstools -i /targetdirectory/target.vmdk -d thin /resultdirectory/result.vmdk

## Kali not updating, failed to fetch http.kali.org
#### Preface:
Kali has officially dropped http support for their package repository and purley use https now.  Some versions may not have the sources.list updated to reflect this.
## Fix:
nano /etc/apt/sources.list
Change:
deb http:// to deb https://

## Powershell v2 [System.Management.Automation.ItemNotFoundException]
#### Preface:
This catch which has become popular in modern PowerShell does not function in v2.  To achieve the same results, use:
Catch [System.Management.Automation.ActionPreferenceStopExecution]

## Get WiFi PSKs from windows devices:
netsh wlan show profile SSID key=clear
Note: This can show ANY WiFi PSK the device has stored, use netsh wlan show profile to get a list of all available SSIDs.
