#!/bin/bash
# Script: my-pi-temp.sh
# ARM CPU and GPU temperature Monitor for Raspberry Pi saved to file
# Author: Paul Richardson Ve9Vw  <http://polymathic.ca/> 
# -------------------------------------------------------
cpu=$(</sys/class/thermal/thermal_zone0/temp)
echo "$(date) @ $(hostname)"
echo "$(tput setaf 2)
       .~~.   .~~.
      '. \ ' ' / .'$(tput setaf 1)
       .~ .~~~..~.    $(tput sgr0)                   _                          _ $(tput setaf 1) 
      : .~.'~'.~. :   $(tput sgr0)   ___ ___ ___ ___| |_ ___ ___ ___ _ _    ___|_|$(tput setaf 1)
     ~ (   ) (   ) ~  $(tput sgr0)  |  _| .'|_ -| . | . | -_|  _|  _| | |  | . | |$(tput setaf 1)
    ( : '~'.~.'~' : ) $(tput sgr0)  |_| |__,|___|  _|___|___|_| |_| |_  |  |  _|_|$(tput setaf 1)
     ~ .~ (   ) ~. ~  $(tput sgr0)              |_|                 |___|  |_|    $(tput setaf 1)
      (  : '~' :  )
       '~ .~~~. ~'
           '~'
$(tput sgr0)"
cat << "EOF"
 (   (                  *    (        *       )     ) (              )  (     
 )\ ))\ )    *   )    (  `   )\ )   (  `   ( /(  ( /( )\ )  *   ) ( /(  )\ )  
(()/(()/(  ` )  /((   )\))( (()/(   )\))(  )\()) )\()|()/(` )  /( )\())(()/(  
 /(_))(_))  ( )(_))\ ((_)()\ /(_)) ((_)()\((_)\ ((_)\ /(_))( )(_)|(_)\  /(_)) 
(_))(_))   (_(_()|(_)(_()((_|_))   (_()((_) ((_) _((_|_)) (_(_())  ((_)(_))   
| _ \_ _|  |_   _| __|  \/  | _ \  |  \/  |/ _ \| \| |_ _||_   _| / _ \| _ \  
|  _/| |     | | | _|| |\/| |  _/  | |\/| | (_) | .` || |   | |  | (_) |   /  
|_| |___|    |_| |___|_|  |_|_|    |_|  |_|\___/|_|\_|___|  |_|   \___/|_|_\  
                                                                              
EOF
echo " Author: Paul Richardson Ve9Vw  <http://polymathic.ca/> under GPL" >> log_temp.txt
echo "-------------------------------------------"
echo "GPU => $(/opt/vc/bin/vcgencmd measure_temp)"
echo "CPU => $((cpu/1000))'C"
echo "Now monitoring every 3 seconds and writing into Log_temp.txt"
echo "Press [ctrl+c] to end monitoring"
echo "Use [cat log_temp.txt] to displays the log contents"
echo "Logfile started: $(date +'%D %T') @ $(hostname)" >> log_temp.txt
while true
do
# vcgencmd measure_temp >> log_temp.txt
echo ",GPU => $(/opt/vc/bin/vcgencmd measure_temp)" >> log_temp.txt
echo ",CPU => $((cpu/1000))'C >>" >> log_temp.txt
echo ",$(date +'%T')" >> log_temp.txt
  	sleep 3
done 
