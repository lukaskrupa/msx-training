# Lab 1 - Using the Development Environment

## Task 1 - Create your VNFD

Using the following [guide](../pg/pg-vnfd.xml) as an example, replace the name of the VNFD to add your name to it, at the same time replace the URL that is being used for the source of the VNFD to the public web server that has been created!

Your XML should look something like this, remember yours should not say LUIS :)
```xml
<?xml version="1.0" encoding="UTF-8"?>
<config xmlns="http://tail-f.com/ns/config/1.0">
  <nfvo xmlns="http://tail-f.com/pkg/tailf-etsi-rel2-nfvo">
  <vnfd>
    <id>LUIS-ISRv</id>
    <provider>Cisco</provider>
    <version>1.2.0</version>
    <product-info-description>Integrated Services Router virtual</product-info-description>
    <vdu>
      <id>ISRv-small</id>
      <description>ISRv Small</description>
      <internal-connection-point-descriptor>
        <id>mgmt</id>
        <external-connection-point-descriptor>mgmt</external-connection-point-descriptor>
        <layer-protocol>IPv4</layer-protocol>
        <interface-id xmlns="http://tail-f.com/pkg/tailf-etsi-rel2-nfvo-nfvis">0</interface-id>
      </internal-connection-point-descriptor>
      <virtual-compute-descriptor>ISR-virtual-small-compute</virtual-compute-descriptor>
      <virtual-storage-descriptor>ISR-virtual-storage</virtual-storage-descriptor>
      <software-image-descriptor>
        <name>ISRv</name>
        <version>16.11.1b</version>
        <container-format>bare</container-format>
        <disk-format>qcow2</disk-format>
        <image>http://135.76.4.80/images/isrv-universalk9.16.11.01b.tar.gz</image>
        <image-name xmlns="http://tail-f.com/pkg/tailf-etsi-rel2-nfvo-nfvis">ISRv</image-name>
        <additional-setting xmlns="http://tail-f.com/pkg/tailf-etsi-rel2-nfvo-nfvis">
          <id>disk_bus</id>
          <value>virtio</value>
        </additional-setting>
        <additional-setting xmlns="http://tail-f.com/pkg/tailf-etsi-rel2-nfvo-nfvis">
          <id>serial_console</id>
          <value>true</value>
        </additional-setting>
      </software-image-descriptor>
      <device-type xmlns="http://tail-f.com/pkg/tailf-etsi-rel2-nfvo-nfvis">
        <cli>
          <ned-id>ios-id:cisco-ios</ned-id>
          <protocol>ssh</protocol>
        </cli>
      </device-type>
      <day0 xmlns="http://tail-f.com/pkg/tailf-etsi-rel2-nfvo-nfvis">
        <destination>ovf-env.xml</destination>
      </day0>
      <day0 xmlns="http://tail-f.com/pkg/tailf-etsi-rel2-nfvo-nfvis">
        <destination>iosxe_config.txt</destination>
        <mandatory/>
      </day0>
    </vdu>
    <virtual-compute-descriptor>
      <id>ISR-virtual-small-compute</id>
      <virtual-memory>
        <virtual-memory-size>4.0</virtual-memory-size>
      </virtual-memory>
      <virtual-cpu>
        <number-of-virtual-cpus>2</number-of-virtual-cpus>
      </virtual-cpu>
    </virtual-compute-descriptor>
    <virtual-storage-descriptor>
      <id>ISR-virtual-storage</id>
      <type-of-storage>root</type-of-storage>
      <size-of-storage>8</size-of-storage>
    </virtual-storage-descriptor>
    <virtual-link-descriptor>
      <id>mgmt</id>
      <connectivity-type>
        <layer-protocol>IPv4</layer-protocol>
      </connectivity-type>
    </virtual-link-descriptor>
    <external-connection-point-descriptor>
      <id>mgmt</id>
      <virtual-link-descriptor>mgmt</virtual-link-descriptor>
      <layer-protocol>IPv4</layer-protocol>
      <management xmlns="http://tail-f.com/pkg/tailf-etsi-rel2-nfvo-nfvis"/>
    </external-connection-point-descriptor>
    <deployment-flavor>
      <id>LUIS-ISRv</id>
      <vdu-profile>
        <vdu>ISRv-small</vdu>
        <min-number-of-instances>1</min-number-of-instances>
        <max-number-of-instances>1</max-number-of-instances>
      </vdu-profile>
      <instantiation-level>
        <id>LUIS-ISRv</id>
        <vdu-level>
          <vdu>ISRv-small</vdu>
          <number-of-instances>1</number-of-instances>
        </vdu-level>
      </instantiation-level>
      <default-instantiation-level>LUIS-ISRv</default-instantiation-level>
    </deployment-flavor>
  </vnfd>
  </nfvo>
</config>
```

**Hint: You need to change the name in 4 different places**

**Hint: You need to point the URL to the correct server**

## Task 2 - Create your Catalog Deployment

Using the following [guide](../pg/pg-catalog-deployment.xml) as an example, replace the name of the *Catalog Deployment* to add your name to it, at the same time replace the URL that is being used for the source of the day0 to the public web server that has been created!

Your XML should look something like this, remember yours should not say LUIS :)
```xml
<?xml version="1.0" encoding="UTF-8"?>
 <config xmlns="http://tail-f.com/ns/config/1.0">
   <catalog xmlns="http://cisco.com/ns/branch-infra-common">
     <name>vBranch</name>
       <deployment>
         <name>LUIS-ISRv-SIP</name>
         <bootup-time>600</bootup-time>
         <recovery-wait-time>0</recovery-wait-time>
         <single-ip-mode/>
         <var>
           <name>ngio</name>
           <val>enable</val>
         </var>
         <vnfd>
           <name>LUIS-ISRv</name>
           <vdu>
             <name>ISRv-small</name>
           </vdu>
         </vnfd>
         <polling-frequency>15</polling-frequency>
         <vnf-port>22</vnf-port>
         <port-start-range>22051</port-start-range>
         <port-end-range>22054</port-end-range>
         <intangible/>
         <day0-url xmlns="http://cisco.com/ns/branchinfra-nfvo">
           <dstFile>iosxe_config.txt</dstFile>
           <url>http://135.76.4.80/day0/ISRv-ManagedDevice.txt</url>
           <var>
             <name>DNS_SERVER_1</name>
             <val>64.102.6.247</val>
           </var>
           <var>
             <name>DNS_SERVER_2</name>
             <val>171.70.168.183</val>
           </var>
           <var>
             <name>DNS_SERVER_3</name>
             <val>173.36.131.10</val>
           </var>
           <var>
             <name>NTP_SERVER_1</name>
             <val>1.ntp.esl.cisco.com</val>
           </var>
           <var>
             <name>SP_ENABLESECRET_VR</name>
             <val>C1sc0123$</val>
           </var>
           <var>
             <name>SP_LICENSE_BANDWIDTH</name>
             <val>100</val>
           </var>
           <var>
             <name>SP_LICENSE_TOKEN</name>
             <val>NjEzNjZlZTAtOGYwZi00NDE4LTgzOGYtYjkxNzE1ZDFmYTQ3LTE1NjM0ODI2%0AODk2MjZ8RkhWZHJNVTgyenJydmVVYjdOY2RVbHZHVElEMFdad0NCNXZYak5U%0AQWlzST0%3D%0A</val>
           </var>
           <var>
             <name>SSH_PASSWORD</name>
             <val>C1sc0123$</val>
           </var>
           <var>
             <name>SSH_USERNAME</name>
             <val>admin</val>
           </var>
           <var>
             <name>MSX_FQDN</name>
             <val>cxmsxp2i1.ciscovms.com</val>
           </var>
         </day0-url>
         <day0-url xmlns="http://cisco.com/ns/branchinfra-nfvo">
           <dstFile>ovf-env.xml</dstFile>
           <url>http://135.76.4.80/day0/ISRv-SIP-CX-ovf-env.xml</url>
           <var>
             <name>SSH_PASSWORD</name>
             <val>C1sc0123$</val>
           </var>
           <var>
             <name>SSH_USERNAME</name>
             <val>cisco</val>
           </var>
           <var>
             <name>TECH_PACKAGE</name>
             <val>ax</val>
           </var>
         </day0-url>
       </deployment>
   </catalog>
 </config>
```

**Hint: You need to create your own day0 configuration file with the proper NAT configuration that deals with Single IP scenario**

**Hint: Make sure that the catalog deployment calls for the right VNFD and VDU name you created in Task 1**

**Hint: Feel free to experiment with the variable and see what you get 😄**

## Task 3 - Create your Branch-Infra

Using the following [guide](../pg/pg-branch-infra-10.201.146.175.xml) as an example, replace:

- Name of CPE
- Serial number to be used
- mgmt-ip-address must be unique
- Replace HOST_WAN_GATEWAY with 135.76.4.254
- Replace HOST_WAN_IP with the IP of your ENCS
- Replace deployment, vnfd and vdu to match the ones you created in Task 1 and Task 2

Your XML should look something like this, remember yours should not say LUIS :)
```xml
<config xmlns="http://tail-f.com/ns/config/1.0">
  <branch-infra xmlns="http://cisco.com/ns/branch-infra">
    <branch-cpe>
      <name>LUISENCS</name>
      <provider>admin</provider>
      <type>ENCS-Secure</type>
      <username>LJqHOtqQyUfcdEOx</username>
      <password>$8$B3AHoth6MI9ZS0G/7yCHcVh6YqPP4mv1EATNFnJIbJM=</password>
      <serial>FGL205210E6</serial>
      <mgmt-ip-address>10.254.2.69</mgmt-ip-address>
      <var>
        <name>HOST_WAN_GATEWAY</name>
        <val>135.76.4.254</val>
      </var>
      <var>
        <name>HOST_WAN_IP</name>
        <val>135.76.4.16</val>
      </var>
      <var>
        <name>HOST_WAN_IP_CIDRMASK</name>
        <val>24</val>
      </var>
      <var>
        <name>HOST_WAN_IP_MASK</name>
        <val>255.255.255.0</val>
      </var>
      <var>
        <name>INT_MGMT_SUBNET_GW</name>
        <val>10.253.0.1</val>
      </var>
      <var>
        <name>INT_MGMT_SUBNET_INVERSE_MASK</name>
        <val>0.0.0.7</val>
      </var>
      <var>
        <name>INT_MGMT_SUBNET_IP</name>
        <val>10.253.0.0</val>
      </var>
      <var>
        <name>INT_MGMT_SUBNET_NETMASK</name>
        <val>255.255.255.248</val>
      </var>
      <var>
        <name>MGMTHUB_OVERLAY_NET_IP</name>
        <val>10.20.0.0</val>
      </var>
      <var>
        <name>MGMTHUB_OVERLAY_NET_MASK</name>
        <val>255.255.255.0</val>
      </var>
      <var>
        <name>MGMT_IP_ADDRESS</name>
        <val>10.254.2.1</val>
      </var>
      <var>
        <name>MGMT_NET</name>
        <val>10.254.2.1/32</val>
      </var>
      <var>
        <name>VBRANCH_DEVICE_TYPE</name>
        <val>ENCS-Secure</val>
      </var>
      <vnfd>
        <name>NFVIS-ISRv-CX</name>
        <vdu>
          <name>ISRv-small</name>
        </vdu>
      </vnfd>
      <vnf>
        <name>LUIS</name>
        <deployment>LUIS-ISRv-SIP</deployment>
        <vnfd>LUIS-ISRv</vnfd>
        <vdu>ISRv-small</vdu>
        <network>
          <name>wan-net</name>
          <nicid>1</nicid>
        </network>
      </vnf>
    </branch-cpe>
  </branch-infra>
</config>
```

**Hint: You need to create your own day0 configuration file with the proper NAT configuration that deals with Single IP scenario**

**Hint: Make sure that the catalog deployment calls for the right VNFD and VDU name you created in Task 1**

**Hint: Feel free to experiment with the variable and see what you get 😄**
