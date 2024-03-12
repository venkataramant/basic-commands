	curl -H "Host: cka.raman.com" 172.27.92.5

	curl ${k_server}/api/v1/namespaces/apps/pods --insecure  --header "Authorization: Bearer ${token}"