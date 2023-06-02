# process-tree-example
Detecting reverse shell activity in Sysdig Secure Process Tree

Download the app example
```
wget https://raw.githubusercontent.com/n1g3ld0ugla5/process-tree-example/main/web-app.yaml
```
Create the app example
```
kubectl apply -f https://raw.githubusercontent.com/n1g3ld0ugla5/process-tree-example/main/web-app.yaml
```

Do the same for the rogue workload
```
wget https://raw.githubusercontent.com/n1g3ld0ugla5/process-tree-example/main/rogue-attacker.yaml
```

Create the rogue workload in the ```default``` network namespace:
```
kubectl apply -f https://raw.githubusercontent.com/n1g3ld0ugla5/process-tree-example/main/rogue-attacker.yaml
```

## Desired Outcome

<img width="645" alt="Screenshot 2023-06-02 at 11 21 06" src="https://github.com/n1g3ld0ugla5/process-tree-example/assets/109959738/2b41b70a-90a9-440f-b018-0f5f046a7817">

Confirm all pods are running
```
kubectl get pods -A
```

Confirm there's a ```backend``` service in the ```storefront``` namespace: 
```
kubectl get svc -n storefront
```

This is the command that will be executed inside the specified Pod. It starts with ```-- sh -c```, which runs the subsequent command using the shell in the container. <br/>
The command being executed is a ```curl``` command, which makes an ```HTTP POST``` request to service backend with the specified headers and data.
```
kubectl exec -it $(kubectl get po -l app=attacker-app -ojsonpath='{.items[0].metadata.name}') -- sh -c "curl http://backend.storefront.svc.cluster.local:80 -H 'User-Agent: Mozilla/4.0' -XPOST --data-raw 'smk=1234'"
```

Although not mentioned explicitly in the previous command, the ```attacker``` pod contained a 
