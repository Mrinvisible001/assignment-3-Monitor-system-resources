#!/bin/bash

while true; do
  clear
  echo "System Resource Monitor"
  echo "-----------------------"
  echo ""
  echo "CPU Usage :"
  top -bn1 | grep "Cpu(s)" | sed "s/.*, *\([0-9.]*\)%* id.*/\1/" | awk '{print 100 - $1"%"}'
  echo ""
  echo "Memory Usage :"
  free -m | awk 'NR==2{printf "Used: %sMB (%.2f%%), Total: %sMB\n", $3, $3*100/$2, $2 }'
  echo ""
  echo "Disk Usage :"
  df -h | awk '$NF=="/"{printf "Used: %dGB (%s), Total: %dGB (%s)\n", $3, $5, $2, $4}'
  echo ""
  echo "Press 'q' to quit."
  read -t 2 -N 1 input
  if [[ $input = "q" ]] || [[ $input = "Q" ]]; then
    exit 0
  fi
done
