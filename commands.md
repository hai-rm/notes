# Getting logs

```
loguat statefulset/lpalgogw-bnp --tail=20 | fixcolor
re-logs -n lp-int -s "1m ago" -p "crossfire-68*"
re-logs -n lp-int -s "2025/06/24 17:12:24" -p "lpalgogw-bnp*" 
```

# Kubernetes

```
kubectl config get-contexts
kubectl config use-context default
kubectl config use-context switchboard-nonprod
kubectl get namespace

kubectl edit --namespace lp-int statefulset/lpfixgw-scb
kubectl edit --namespace lp-int configmap/lpfixgw-scb-config

kubectl scale --namespace lp-int statefulset/lpfixgw-scb --replicas=0
kubectl scale --namespace lp-int statefulset/lpfixgw-scb --replicas=1
# Or just Ctrl+K in k9s to bounce the pod

kubectl --namespace lp-int port-forward deploy/socat-hchu-marketdata 9021 &
kubectl --namespace lp-int port-forward deploy/socat-hchu-order 9022 &
kubectl --namespace lp-int port-forward service/crossfire-internal 8290 &

kubectl logs --namespace lp-int statefulsets/lpfixgw-scb --tail=2000 | fix2pipe > short.txt
kubectl logs --namespace lp-int statefulsets/lpfixgw-scb --since=5m | ~/codebase/fix2pipexx/fix2pipe++.py -t ~/codebase/reactive-cpp/reactive/fix/Tag.hpp -s name > view.txt

helm uninstall --namespace lp-int lpfixgw-call-rfq
kubectl delete --namespace lp-int pvc/data-lpfixgw-call-rfq-0
```

# Ansible

```
ansible-playbook playbooks/application.yml --inventory inventories/switchboard-uat --ask-vault-pass --extra-vars "helm_chart_filter=crossfire-fix1"
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

# Regression tests

```
codebase/reactive-py/
venv/bin/activate
qa/regression/
make up
export LOCAL_REGRESSION_TEST=ANY_VALUE
pytest -sv client_api/test_agg_md.py::test_non_agg_sub_market_mapping_update_basic
```

# Redis

```
# Logging out and relogging lpfixgw in UAT
[twono@Endeavour ~]$ kubectl port-forward --namespace lp-int svc/lpfixgw-ctdl-internal 6379
[twono@Endeavour ~]$ redis-cli
127.0.0.1:6379> RE.SESS-LIST
127.0.0.1:6379> RE.SESS-ENABLE 4.4:CLI_QUOTES->CIG_QUOTES no
127.0.0.1:6379> RE.SESS-ENABLE 4.4:CLI_QUOTES->CIG_QUOTES yes

# Checking sim data in INT
$ kubectl port-forward svc/redis-analytics-slave 6379 -n int
$ redis-cli
> XREVRANGE data.ohlc.stream:EURSEK-REX:1s + - COUNT 1
```

# PCAP

```
# in switchup
script/re-openpcap -n ny4 -s "2024/08/12 19:43:00" -e "2024/08/12 19:44:20" -a 10.130.221.52 -p 8909
```

# SBE

```
~/go/bin/re-sbe-tool -go ~/codebase/schema/sbe/schema.xml | gofmt -s > ~/codebase/reactive-go/pkg/encoding/sbe/schema.go
~/go/bin/re-sbe-tool -cpp ~/codebase/schema/sbe/schema.xml | clang-format --style=file:/home/twono/codebase/reactive-cpp/.clang-format > ~/codebase/reactive-cpp/reactive/sbe/Schema.hpp
```
