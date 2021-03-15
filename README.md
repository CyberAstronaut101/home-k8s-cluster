# Home K8s Cluster

This is a repo to hold various deployments for my home microk8s cluster with 4x RPi 4 8GB worker nodes. 

`journalctl -u snap.microk8s.daemon-kubelet`


# Pod not scheduling?
```bash
kubectl get nodes -o wide
kubectl get events

// View Logs
kubectl logs <POD_NAME>
```



# Aliases

`.bash_aliases
```
alias kubedebug="kubectl run -i --tty --rm debug --image=busybox --restart=Never --"
```
https://betterprogramming.pub/useful-kubectl-aliases-that-will-speed-up-your-coding-54960185d10`

https://www.jeffgeerling.com/blog/2020/raspberry-pi-cluster-episode-4-minecraft-pi-hole-grafana-and-more

https://www.careyscloud.ie/pihole_metallb

https://github.com/carlosedp/cluster-monitoring#quickstart-for-k3s