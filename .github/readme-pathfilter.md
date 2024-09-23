# logs-gateway

include-paths: "['cmd/logs-gateway/**', 'pkg/cloud/logs/gateway*']"
exclude-paths: "['dummy']"

- change cmd/logs-gateway/** -> trigger deploy-logs-gateway
- change pkg/cloud/logs/gateway* -> trigger deploy-logs-gateway
- change pkg/cloud/logs/** -> don't trigger deploy-logs-gateway
- change cmd/logs-gateway/** and pkg/cloud/logs/gateway* -> trigger deploy-logs-gateway
- change cmd/logs-gateway/** and pkg/cloud/logs/** -> trigger deploy-logs-gateway
- change cmd/logs-gateway/** and pkg/cloud/logs/gateway* and pkg/cloud/logs/** -> trigger deploy-logs-gateway

```
msg="1: logs-gateway: change cmd/logs-gateway/** -> trigger deploy-logs-gateway"
echo $msg
echo foo >> cmd/logs-gateway/logs-gateway
git add .
git commit -sm $msg
git push origin main


msg="2: logs-gateway: change pkg/cloud/logs/gateway* -> trigger deploy-logs-gateway"
echo $msg
echo foo >> pkg/cloud/logs/gateway-foo
git add .
git commit -sm $msg
git push origin main


msg="3: logs-gateway: change pkg/cloud/logs/** -> don't trigger deploy-logs-gateway"
echo $msg
echo foo >> pkg/cloud/logs/not-gateway-foo
git add .
git commit -sm $msg
git push origin main

msg="4: logs-gateway: change cmd/logs-gateway/** and pkg/cloud/logs/gateway* -> trigger deploy-logs-gateway"
echo $msg
echo foo >> cmd/logs-gateway/logs-gateway
echo foo >> pkg/cloud/logs/gateway-foo
git add .
git commit -sm $msg
git push origin main

msg="5: logs-gateway: change cmd/logs-gateway/** and pkg/cloud/logs/** -> trigger deploy-logs-gateway"
echo $msg
echo foo >> cmd/logs-gateway/logs-gateway
echo foo >> pkg/cloud/logs/not-gateway-foo
git add .
git commit -sm $msg
git push origin main

msg="6: logs-gateway: change cmd/logs-gateway/** and pkg/cloud/logs/gateway* and pkg/cloud/logs/** -> trigger deploy-logs-gateway"
echo $msg
echo foo >> cmd/logs-gateway/logs-gateway
echo foo >> pkg/cloud/logs/gateway-foo
echo foo >> pkg/cloud/logs/not-gateway-foo
git add .
git commit -sm $msg
git push origin main
```

# logs-forwarder

include-paths: "['cmd/logs-forwarder/**', 'pkg/cloud/logs/**']"
exclude-paths: "[ 'pkg/cloud/logs/gateway*' ]"

- change cmd/logs-forwarder/** -> trigger deploy-logs-forwarder
- change pkg/cloud/logs/** -> trigger deploy-logs-forwarder
- change pkg/cloud/logs/gateway* -> don't trigger deploy-logs-forwarder
- change cmd/logs-forwarder/** and pkg/cloud/logs/** -> trigger deploy-logs-gateway
- change cmd/logs-forwarder/** and pkg/cloud/logs/gateway* -> trigger deploy-logs-gateway
- change cmd/logs-forwarder/** and change pkg/cloud/logs/** and pkg/cloud/logs/gateway* -> trigger deploy-logs-gateway

```
msg="1: logs-forwarder: logs-forwarder: change cmd/logs-forwarder/** -> trigger deploy-logs-forwarder"
echo $msg
echo foo >> cmd/logs-forwarder/logs-forwarder
git add .
git commit -sm $msg
git push origin main


msg="2: logs-forwarder: change pkg/cloud/logs/** -> trigger deploy-logs-forwarder"
echo $msg
echo foo >> pkg/cloud/logs/anything-foo
git add .
git commit -sm $msg
git push origin main


msg="3: logs-forwarder: change pkg/cloud/logs/gateway* -> don't trigger deploy-logs-forwarder"
echo $msg
echo foo >> pkg/cloud/logs/gateway-foo
git add .
git commit -sm $msg
git push origin main

msg="4: logs-forwarder: change cmd/logs-forwarder/** and pkg/cloud/logs/** -> trigger deploy-logs-forwarder"
echo $msg
echo foo >> cmd/logs-forwarder/logs-forwarder
echo foo >> pkg/cloud/logs/anything-foo
git add .
git commit -sm $msg
git push origin main

msg="5: logs-forwarder: change cmd/logs-forwarder/** and pkg/cloud/logs/gateway* -> trigger deploy-logs-forwarder"
echo $msg
echo foo >> cmd/logs-forwarder/logs-forwarder
echo foo >> pkg/cloud/logs/gateway-foo
git add .
git commit -sm $msg
git push origin main

msg="6: logs-forwarder: change cmd/logs-forwarder/** and pkg/cloud/logs/** and pkg/cloud/logs/gateway* -> trigger deploy-logs-forwarder"
echo $msg
echo foo >> cmd/logs-forwarder/logs-forwarder
echo foo >> pkg/cloud/logs/anything-foo
echo foo >> pkg/cloud/logs/gateway-foo
git add .
git commit -sm $msg
git push origin main

msg="7: logs-forwarder: change pkg/cloud/logs/** and pkg/cloud/logs/gateway* -> trigger deploy-logs-forwarder"
echo $msg
echo foo >> pkg/cloud/logs/anything-foo
echo foo >> pkg/cloud/logs/gateway-foo
git add .
git commit -sm $msg
git push origin main

msg="8: logs-forwarder: change pkg/cloud/logs/** and multiple pkg/cloud/logs/gateway* -> trigger deploy-logs-forwarder"
echo $msg
echo foo >> pkg/cloud/logs/anything-foo
echo foo >> pkg/cloud/logs/gateway-foo
echo foo >> pkg/cloud/logs/gateway-bar
git add .
git commit -sm $msg
git push origin main

msg="9: logs-forwarder: change multiple pkg/cloud/logs/gateway* -> don't trigger deploy-logs-forwarder"
echo $msg
echo foo >> pkg/cloud/logs/gateway-foo
echo foo >> pkg/cloud/logs/gateway-bar
git add .
git commit -sm $msg
git push origin main
```