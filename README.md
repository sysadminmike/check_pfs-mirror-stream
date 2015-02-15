# check_pfs-mirror-stream
Nagios check for hammer pfs mirror stream

Checks the difference between master and slave sync-end-tid.

     check_pfs-mirror-stream -m <master_pfs> -s <slave_pfs> [-d <difference warning>] [-w <wait time>] [-p master "pfs ssh opts"] [-q "slave pfs ssh opts"]
     
difference warning
Is how far apart the master sync-end-tid and slave sync-end-tid can be before plugin exits with WARNING exit code (default: 5000)

wait time
Is the time to sleep for between first checking a slave pfs sync-end-tid and the next check of the slave pfs sync-end-tid to see if it is changing (default: 8 seconds)

Example Status Information:

     ERROR - master:/home:0x000000011020e890, slave:/BACKUP/pfs/home:0x000000010ff2f300 not increasing, difference: 3011984. 

     WARNING tid difference above threashold - master:/home:0x000000011020e890, slave:/BACKUP/pfs/home:0x000000010ff2f301, difference: 2014983. 

     OK syncing - master:/home:0x000000011020e890, slave:/BACKUP1/pfs/home:0x000000011020e870, difference: 32.

     OK synced - master:/home:0x000000010fa4b880, slave:/BACKUP/pfs/home:0x000000010fa4b880


Checking on with both local master and slave:

     check_pfs-mirror-stream -m /home -s /BACKUP/pfs/home
 

Checking on slave with remote master:

     check_pfs-mirror-stream -m 192.168.0.100:/home -s /BACKUP/pfs/home -p '-i/home/nagios/mykey'
 

Checking on master with remote slave:

     check_pfs-mirror-stream -m /home -s 192.168.0.101:/BACKUP/pfs/home -q '-i/home/nagios/mykey'
 

Checking on with both remote master and slave:

     check_pfs-mirror-stream -m 192.168.0.100:/home -s 192.168.0.101:/BACKUP/pfs/home -p '-i/home/nagios/mykey' -q '-i/home/nagios/mykey'
 
 
 Note: the remote pfs checking does work but it is fiddly to get ssh setup correctly and you need to use the same user throughout as -p and -q are not passing properly.
 
