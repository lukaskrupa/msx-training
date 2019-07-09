# Creating a Template

## Onboard a device into NSO

Apply configuration found [here](./add-nso-device.xml), replace the IPs and passwords with the ones for your device.

Once onboarded from NSO execute:

```
admin@ncs# devices device MDTEST ssh fetch-host-keys
result updated
fingerprint {
    algorithm ssh-rsa
    value 3a:97:e1:e3:f6:4d:0a:f8:5d:2c:b0:ac:4a:24:d3:c1
}
admin@ncs# devices device MDTEST sync-from
result true
```

## Convert the Configuration to a Template

Apply the configuration you want to convert into template directly on the device.

```
CISCOCXTEST-ISRv#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
CISCOCXTEST-ISRv(config)#inter
CISCOCXTEST-ISRv(config)#interface loopback 0
CISCOCXTEST-ISRv(config-if)#desc
CISCOCXTEST-ISRv(config-if)#description Managed Device Loopback
CISCOCXTEST-ISRv(config-if)#ip address 19.19.19.19 255.255.255.255
CISCOCXTEST-ISRv(config-if)#^Z
```

From NSO compare the config in CDB with the config on the device, select XML as the output format:

```
admin@ncs# devices device MDTEST compare-config outformat xml
diff
<devices xmlns="http://tail-f.com/ns/ncs">
  <device>
    <name>MDTEST</name>
    <config>
      <interface xmlns="urn:ios">
        <Loopback>
          <name>0</name>
          <description>Managed Device Loopback</description>
          <ip>
            <address>
              <primary>
                <address>19.19.19.19</address>
                <mask>255.255.255.255</mask>
              </primary>
            </address>
          </ip>
        </Loopback>
      </interface>
    </config>
  </device>
</devices>
```

Replace the device name with *{$DEVICE_NAME}* and add the *<config>* tag and anything you want to convert to variables.
The config should look like this:

```xml
<config xmlns="http://tail-f.com/ns/config/1.0">
  <devices xmlns="http://tail-f.com/ns/ncs">
    <device>
      <name>{$DEVICE_NAME}</name>
      <config>
        <interface xmlns="urn:ios">
          <Loopback>
            <name>0</name>
            <description>{$LOOPBACK_DESCRIPTION}</description>
            <ip>
              <address>
                <primary>
                  <address>{$LOOPBACK_IPV4}</address>
                  <mask>255.255.255.255</mask>
                </primary>
              </address>
            </ip>
          </Loopback>
        </interface>
      </config>
    </device>
  </devices>
</config>
```

Save the file with XML extension and upload to MSX. An example can be found [here](../../cx_loopback.xml)
