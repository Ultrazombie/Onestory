1. create folder scripts in directory /etc/init.d/
   > touch /etc/init.d/scripts
2. add premmissions for writiing for that folder
   > chmod 777 /etc/init.d/scripts
3. create bash script file for start rethinkDB
   vi /etc/init.d/scripts/DB.sh
   #!/bin/bash
   rethinkdb
4. create bash script file for start STF
   vi /etc/init.d/scripts/stf.sh
   #!/bin/bash
   stf local --public-ip 192.168.88.213
5. add scripts to autostart (daemoon)
   vi /etc/systemd/system/DB.service
   [Unit]
   Description=DB
   After=multi-user.target
   [Service]
   Type=idle
   ExecStart=/etc/init.d/scripts/DB.sh
   Restart=always
   [Install]
   WantedBy=multi-user.target
   vi /etc/systemd/system/stf.service
   [Unit]
   Description=STF
   After=multi-user.target
   [Service]
   Type=idle
   ExecStart=/etc/init.d/scripts/stf.sh
   Restart=always
   [Install]
   WantedBy=multi-user.target
6. systemctl enable DB.service
7. systemctl enable stf.service
8. restart PC.
