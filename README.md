# k3s

### install k3s on linux machine using sh script using args
	$ curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION=v0.3.0 sh -


### Upgrade to an RC version 
	$ curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION=v0.7.0-rc4 sh -

### Upgrade to an RC verison with no sudo permissions 
	$ curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION=v0.7.0-rc4 INSTALL_K3S_EXEC="--write-kubeconfig-mode 644" sh -

### Install the lates version of k3s 
	$ curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC="--write-kubeconfig-mode 644" sh -

<br />
# Prepare Server side only (Without agent)
### create the k3s server
	$ curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC="--disable-agent --write-kubeconfig-mode 644 --tls-san <pub-ip-srv-add>" sh - 
### Genarate the token from the server side 
	$ echo "export node_token=$(sudo cat /var/lib/rancher/k3s/server/node-token)"
<br />
# Prepare the Agent side.
### create the agent using binery
	$ curl -L -o k3s https://github.com/rancher/k3s/releases/download/v0.6.1/k3s
### change the mode and move it to /local/bin
	$ chmod 755 k3s && mv k3s /usr/local/bin/k3s 
### Paste the output from the echo command on the agent side
	$ export node_token=34932409238493482390-SOME-EXAMPLE-OF-TOKEN-3294324098234324230-4823

### Run k3s on the agent by specify the agent mode and the token that we export previously
	$ sudo /usr/local/bin/k3s agent --server https://<pub-ip-srv-add>:6443 --token "$node_token" >& k3s-agent.log &
<br />
### Check the node on the server side. 
	$ kubectl get pods 




<br />
<br />

