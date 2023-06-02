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

<img width="645" alt="Screenshot 2023-06-02 at 11 21 06" src="https://github.com/n1g3ld0ugla5/process-tree-example/assets/109959738/2b41b70a-90a9-440f-b018-0f5f046a7817">
