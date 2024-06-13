# Ansible

```
ansible-playbook playbooks/aws_cluster.yml --inventory inventories/switchboard-uat --ask-vault-pass --extra-vars "helm_chart_filter=crossfire-fix1"
```

# Docker

```
[twono@Endeavour ~]$ docker run -it --rm 120885552157.dkr.ecr.eu-west-2.amazonaws.com/reactive-cpp:hchu lpfixgw

# if not specifying lpfixgw then run inside the container (useful if we want to modify the config files)
root@13e840b7f355:/# /cpp/bin/re-lpfixgw -f /cpp/etc/lpfixgw.conf
```
Once in a while:
```
docker system prune
```

# Kubernetes

```
kubectl config use-context default

kubectl edit --namespace uat statefulset/lpfixgw-scb
kubectl edit --namespace uat configmap/lpfixgw-scb-config

kubectl scale --namespace uat statefulset/lpfixgw-scb --replicas=0
kubectl scale --namespace uat statefulset/lpfixgw-scb --replicas=1
# Or just Ctrl+K in k9s to bounce the pod

kubectl logs --namespace uat statefulsets/lpfixgw-scb --tail=2000 | fix2pipe > short.txt
kubectl logs --namespace uat statefulsets/lpfixgw-scb --since=5m | ~/codebase/fix2pipexx/fix2pipe++.py -t ~/codebase/reactive-cpp/reactive/fix/Tag.hpp -s name > view.txt
```

# SBE

```
~/go/bin/re-sbe-tool -go ~/codebase/schema/sbe/schema.xml | gofmt -s > ~/codebase/reactive-go/pkg/encoding/sbe/schema.go
~/go/bin/re-sbe-tool -cpp ~/codebase/schema/sbe/schema.xml | clang-format --style=file:/home/twono/codebase/reactive-cpp/.clang-format > ~/codebase/reactive-cpp/reactive/sbe/Schema.hpp
```
