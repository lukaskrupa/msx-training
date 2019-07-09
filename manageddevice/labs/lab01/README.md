# Lab 1 - Deploy a Template to a Managed Device

## Task 1 - Create an XML Template to Upload
The first process in uploading a template is creation of the template. This involves understand what we want to accomplish with the template.

In order to accomplish this and understanding of how to convert a configuration from the device's native configuration language to XML is required. An aid that can be used here is to onboard a device to NSO and apply the configuration using native device commands and then *sync-from* the device in NSO to display the XML equivalent of the configuration. Check Appendix A for information on how to accomplish this.

For now we will apply a configuration to a device that creates a syslog entry on the device so that syslog messages are sent to a specific server.

The following XML will be used:
```xml
<config xmlns="http://tail-f.com/ns/config/1.0">
  <devices xmlns="http://tail-f.com/ns/ncs">
  <device>
    <name>{$DEVICE_NAME}</name>
      <config>
      <logging xmlns="urn:ios">
        <hostname>
          <host>{$SYSLOG_SERVER}</host>
        </hostname>
        <source-interface>
          <name>Tunnel0</name>
          <vrf>MGMT-OVERLAY</vrf>
        </source-interface>
      </logging>
      </config>
  </device>
  </devices>
</config>
```

For now lets create a file and copy the contents of the above XML to it.

## Task 2 - Upload Template to MSX

Following the process explained during the presentation, upload your XML to MSX.

## Text 3 - Deploy a Template on a Managed Device

Go through the process of ordering a template for your device.
