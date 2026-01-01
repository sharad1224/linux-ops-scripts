# linux-ops-scripts

## 🚀 Script: CPU info



#!/bin/bash
# This line tells the system to use Bash to run the script.

echo "Current CPU Load Average:"
uptime | awk -F'load average:' '{ print $2 }'



# Help with Shell script that monitors CPU Usage
#!/bin/ksh
top -b -n 1 |head -8 >/tmp/cpu.text
sed -e '1,5d' /tmp/cpu.text >/tmp/cpu2.text
High_CPU=`cat /tmp/cpu2.text|tail -1|awk '{print $9}'`
host=`hostname`
if [ "$High_CPU -gt  90" ];
then
mail -s "High CPU USAGE on $host" test@test.comv < /tmp/cpu2.lst
fi
exit;




