# Ansible

```
ansible-playbook playbooks/aws_cluster.yml --inventory inventories/switchboard-uat --ask-vault-pass --extra-vars "helm_chart_filter=crossfire-fix1"
```

# git

```
# Squashing commits
git reset --soft HEAD~1
git push --force-with-lease origin <branch-name>
```

# Kubernetes

```
kubectl config use-context default

kubectl edit --namespace uat statefulset/lpfixgw-scb
kubectl edit --namespace uat configmap/lpfixgw-scb-config

kubectl scale --namespace uat statefulset/lpfixgw-scb --replicas=0
kubectl scale --namespace uat statefulset/lpfixgw-scb --replicas=1
# or just Ctrl+K in k9s to bounce the pod

kubectl logs --namespace uat statefulsets/lpfixgw-scb --tail=2000 | fix2pipe > short.txt
kubectl logs --namespace uat statefulsets/lpfixgw-scb --since=5m | ~/codebase/fix2pipexx/fix2pipe++.py -t ~/codebase/reactive-cpp/reactive/fix/Tag.hpp -s name > view.txt
```
