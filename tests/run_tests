#!/usr/bin/env bash

RED='\033[0;31m'
COUNT=15
while [ $COUNT -gt 0 ]; do
    printf "$COUNT "
    sleep 0.1
    let COUNT=COUNT-1
done
printf "\nINFO: Test completed, 1 test FAILED, 10 total actions\n"
dd bs=1M count=10 if=/dev/urandom of=error.txt status=none
printf "${RED}See error.txt for more info\n"
exit 1
