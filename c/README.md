## res_pbxhelper.c
If you use an explicit transport definition in endpoints, you will not get the transport name in the dialplan. This module assigns the transport name on the incoming channel to the channel variable named "TRANSPORT_ID". It works only on the incoming channel.

``` bash
exten => n,NoOp(${TRANSPORT_ID})

    -- Executing [1001@from-inside:2] NoOp("PJSIP/1001-00000000", "transportX") in new stack
```

``` config
[transportX]
type=transport
bind=x.x.x.x:5060
protocol=udp

[transportY]
type=transport
bind=y.y.y.y:5060
protocol=udp

[1001]
type=endpoint
aors=1001
auth=1001
callerid="User 1001" <1001>
context=from-inside

[1001]
type=auth
auth_type=userpass
password=1234567
username=1001

[1001]
type=aor
max_contacts=3
qualify_frequency=60
qualify_timeout=6.0
```
