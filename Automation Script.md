# linux-ops-scripts

## 🚀 Script: CPU info



#!/bin/bash
# This line tells the system to use Bash to run the script.

echo "Current CPU Load Average:"
uptime | awk -F'load average:' '{ print $2 }'




