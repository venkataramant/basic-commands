# echo "Please wait while the environments are set up..."; 
	while [ ! -f /opt/.backgroundfinished ]; do sleep 2; 
	done; 
	echo "Ready!"