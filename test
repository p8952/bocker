#!/usr/bin/env bash

exit_code=0
for t in tests/test_*; do
	bash tests/teardown > /dev/null 2>&1
	bash "$t" > /dev/null 2>&1
	if [[ $? == 0 ]]; then
		echo -e "\e[1;32mPASSED\e[0m : $t"
	else
		echo -e "\e[1;31mFAILED\e[0m : $t"
		exit_code=1
	fi
	bash tests/teardown > /dev/null 2>&1
done
exit "$exit_code"
