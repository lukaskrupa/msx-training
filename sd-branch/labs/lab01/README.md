# Lab 1 - Using the Development Environment

# Task 1 - Create your VNFD

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

# Task 2 -
