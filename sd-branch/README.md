# Tips & Tricks

## Connecting to vmConsole from an ENCS Console

Use a different escape character to connect to ENCS' console that way ^]
```
telnet -e ^Q ENCS_AND_PORT
```

## vBranch CFP Commands

### Checking branch-cpe plan

`show branch-infra:branch-infra-status branch-cpe <NAME> plan`

```
admin@ncs# show branch-infra:branch-infra-status branch-cpe CISCOCXTEST plan
                                                                                                                                       VM
NAME         TYPE        REAL NAME    CPE  PROVIDER  TENANT  IMAGE  FLAVOR  VDU  VDUS  VNFD  VNF  DEVICE                   DEPLOYMENT  GROUP  STATE         STATUS   WHEN                 ref  MESSAGE
-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
self         self        CISCOCXTEST  -    -         -       -      -       -    -     -     -    -                        -           -      init          reached  2019-07-09T07:41:33  -
                                                                                                                                              ready         reached  2019-07-09T07:46:27  -
CISCOCXTEST  branch-cpe  CISCOCXTEST  -    admin     -       -      -       -    -     -     -    CISCOCXTEST_ENCS-Secure  -           -      init          reached  2019-07-09T07:41:33  -
                                                                                                                                              pnp-callhome  reached  2019-07-09T07:41:33  -
                                                                                                                                              ready         reached  2019-07-09T07:46:27  -    Ready in secure_overlay mode
```

### Connect to NSO

`ncs_cli -u admin -C`

### Clean Up of ENCS on NSO

`branch-infra service-cleanup branchcpe <NAME>`

## NFVIS Commands

### Checking Secure-Overlay

`show secure-overlay`

```
CISCOCXTEST# show secure-overlay
                ACTIVE
                LOCAL   STATE
NAME     STATE  BRIDGE  DETAILS
---------------------------------
mgmtvpn  up     wan-br
```

### Cleanup of NFVIS after a failed deployment

1. Remove deployments `no vm_lifecycle tenants tenant admin deployments deployment <NAME>`
2. Remove single-ip-mode `no single-ip-mode`
3. Remove secure-overlay `no secure-overlay`
4. Remove users created by NSO
5. Remove networks created by NSO
6. Remove images created by NSO
7. Remove flavors created by NSO
8. Restart PnP Client `pnp action command restart`
