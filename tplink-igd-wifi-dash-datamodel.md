<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<DeviceModel name="TP-Link_IGD_CABO" manufacturer="TP-Link_IGD_CABO" oui="5CA6E6,003192,005F67,3C846A,50D4F7,6032B1,60A4B7,6C5AB0,74DA88,84D81B,C006C3,C0C9E3,CC32E5,D807B6,D84732,E4C32A" productClass="IGD" objectModelDefinitions="InternetGatewayDevice:1.1" description="" setNotification="true" setAccessList="true" protocolType="TR069">
    <supportedRPCMethods>DeleteObject</supportedRPCMethods>
    <supportedRPCMethods>GetParameterNames</supportedRPCMethods>
    <supportedRPCMethods>GetParameterAttributes</supportedRPCMethods>
    <supportedRPCMethods>Upload</supportedRPCMethods>
    <supportedRPCMethods>AddObject</supportedRPCMethods>
    <supportedRPCMethods>GetParameterValues</supportedRPCMethods>
    <supportedRPCMethods>Reboot</supportedRPCMethods>
    <supportedRPCMethods>SetParameterAttributes</supportedRPCMethods>
    <supportedRPCMethods>GetRPCMethods</supportedRPCMethods>
    <supportedRPCMethods>ScheduleInform</supportedRPCMethods>
    <supportedRPCMethods>SetParameterValues</supportedRPCMethods>
    <supportedRPCMethods>Download</supportedRPCMethods>
    <supportedRPCMethods>FactoryReset</supportedRPCMethods>
    <options dashboardDevicePollTime="10" reloadOnFactoryReset="ALWAYS" collectConnectedDevices="false" deviceType="RGW" addObjectBackfill="true" discoveryRetry="0" simpleDiscoveryRetry="3" simpleDiscoveryEnabled="false"/>
    <deviceServiceConfigurations name="DHCP">
        <scriptDefinition name="TP-Link_IGD_LAB: DHCP" purpose="Device service configuration" tags="null" scriptParameters="[]">
            <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var data = {
  label: "DHCP",
  parameters: [
    { label:"Enable DHCP service", cpeParameterName:"InternetGatewayDevice.LANDevice.1.LANHostConfigManagement.DHCPServerEnable" },
    { label:"DNS Servers", cpeParameterName:"InternetGatewayDevice.LANDevice.1.LANHostConfigManagement.DNSServers" },
    { label:"DHCP Start Address", cpeParameterName:"InternetGatewayDevice.LANDevice.1.LANHostConfigManagement.MinAddress" },
    { label:"DHCP End Address", cpeParameterName:"InternetGatewayDevice.LANDevice.1.LANHostConfigManagement.MaxAddress" },
    { label:"Lease Time", cpeParameterName:"InternetGatewayDevice.LANDevice.1.LANHostConfigManagement.DHCPLeaseTime" }, 
    { label:"LAN IP Address", cpeParameterName:"InternetGatewayDevice.LANDevice.1.LANHostConfigManagement.IPInterface.1.IPInterfaceIPAddress" }
  ]
};

var response = dsc.createResponse({
    data: data,
    scriptParameters: scriptParameters
});

response;
</javaScriptCode>
        </scriptDefinition>
    </deviceServiceConfigurations>
    <deviceServiceConfigurations name="WAN">
        <scriptDefinition name="TP-Link_IGD_LAB: WAN" purpose="Device service configuration" tags="null" scriptParameters="[]">
            <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var conditionalRendering = [
  {
    group: "Static Addressing Type",
    dependsOnParameter: "Addressing Type",
    showOnValue: ["Static"]
  }
];

var AddressingTypeDatatype = {
  type: "ENUM",
  choice: [
    { systemName: "DHCP", friendlyName: "DHCP" },
    { systemName: "Static", friendlyName: "Static" }
  ]
};

var data = {
  label: "WAN",
  parameters: [
    { label: "WANAccessType", cpeParameterName:"InternetGatewayDevice.WANDevice.1.WANCommonInterfaceConfig.WANAccessType" },
    { label: "PhysicalLinkStatus", cpeParameterName:"InternetGatewayDevice.WANDevice.1.WANCommonInterfaceConfig.PhysicalLinkStatus" },
    { label: "MAC Address", cpeParameterName:"InternetGatewayDevice.WANDevice.1.WANConnectionDevice.1.WANIPConnection.1.MACAddress" },
    { label: "DNS Servers", cpeParameterName:"InternetGatewayDevice.WANDevice.1.WANConnectionDevice.1.WANIPConnection.1.DNSServers" },
    { label: "Layer1DownstreamMaxBitRate", cpeParameterName:"InternetGatewayDevice.WANDevice.1.WANCommonInterfaceConfig.Layer1DownstreamMaxBitRate" },
    { label: "Layer1UpstreamMaxBitRate", cpeParameterName:"InternetGatewayDevice.WANDevice.1.WANCommonInterfaceConfig.Layer1UpstreamMaxBitRate" },
    { label: "TotalBytesReceived", cpeParameterName:"InternetGatewayDevice.WANDevice.1.WANCommonInterfaceConfig.TotalBytesReceived" },
    { label: "TotalBytesSent", cpeParameterName:"InternetGatewayDevice.WANDevice.1.WANCommonInterfaceConfig.TotalBytesSent" },
    { label: "TotalPacketsReceived", cpeParameterName:"InternetGatewayDevice.WANDevice.1.WANCommonInterfaceConfig.TotalPacketsReceived" },
    { label: "TotalPacketsSent", cpeParameterName:"InternetGatewayDevice.WANDevice.1.WANCommonInterfaceConfig.TotalPacketsSent" },
    { label: "Addressing Type", cpeParameterName:"InternetGatewayDevice.WANDevice.1.WANConnectionDevice.1.WANIPConnection.1.AddressingType", dataType: AddressingTypeDatatype },
    { label: "External IP Address", cpeParameterName:"InternetGatewayDevice.WANDevice.1.WANConnectionDevice.1.WANIPConnection.1.ExternalIPAddress", group: "Static Addressing Type" },
    { label: "Gateway Address", cpeParameterName:"InternetGatewayDevice.WANDevice.1.WANConnectionDevice.1.WANIPConnection.1.DefaultGateway", group: "Static Addressing Type" }
  ]
};

var response = dsc.createResponse({
  data: data,
  scriptParameters: scriptParameters,
  conditionalRendering: conditionalRendering
});

response;
</javaScriptCode>
        </scriptDefinition>
    </deviceServiceConfigurations>
    <deviceServiceConfigurations name="WiFi 2">
        <scriptDefinition name="TP-Link_IGD_LAB: WiFi 2" purpose="Device service configuration" tags="null" scriptParameters="[]">
            <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var channelDataType = {
  type: "ENUM", 
  choice:[
    { systemName: "0", friendlyName: "auto" },
    { systemName: "1", friendlyName: "1" },
    { systemName: "2", friendlyName: "2" },
    { systemName: "3", friendlyName: "3" },
    { systemName: "4", friendlyName: "4" },
    { systemName: "5", friendlyName: "5" },
    { systemName: "6", friendlyName: "6" },
    { systemName: "7", friendlyName: "7" },
    { systemName: "8", friendlyName: "8" },
    { systemName: "9", friendlyName: "9" },
    { systemName: "10", friendlyName: "10" },
    { systemName: "11", friendlyName: "11" }
  ]
};

var conditionalRendering = [
  {
    group: "WEP-Open",
    dependsOnParameter: "SecurityMode",
    showOnValue: ["WEP-Open"]
  },
  {
    group: "WEP-Shared",
    dependsOnParameter: "SecurityMode",
    showOnValue: ["WEP-Shared"]
  },
  {
    group: "WPA",
    dependsOnParameter: "SecurityMode",
    showOnValue: ["TKIPEncryption", "AESEncryption", "TKIPandAESEncryption"]
  }
];

var data = {
  label: "WiFi",
  parameters: [
    { label: "SSID", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.SSID" },
    { label: "Enabled", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Enable" },
    { label: "Broadcast SSID", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.BeaconAdvertisementEnabled" },
    { label: "Channel", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel", dataType: channelDataType },
    { label: "Current Password Index", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKeyIndex", groups: ["WEP-Open", "WEP-Shared"] },
    { label: "Password 1", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.1.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    { label: "Password 2", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.2.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    { label: "Password 3", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.3.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    { label: "Password 4", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.4.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    { label: "Password", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.PreSharedKey.1.PreSharedKey", group: "WPA" },
    { label: "WPAA uthentication Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WPAAuthenticationMode", internalOnly: true },
    { label: "WPA Encryption Modes", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WPAEncryptionModes", internalOnly: true },
    { label: "Basic Authentication Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.BasicAuthenticationMode", internalOnly: true },
    { label: "Basic Encryption Modes", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.BasicEncryptionModes", internalOnly: true },
    { label: "Beacon Type", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.BeaconType", internalOnly: true },
    { label: "Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Standard", internalOnly: true },
    { label: "Mode", description: "Standard Mode", readCallback: readStandardModeCallback, writable: false },
    { label: "Security Mode", description: "Security Mode", readCallback: readSecurityModeCallback }
  ]
};

var response = dsc.createResponse({
  data: data,
  scriptParameters: scriptParameters,
  customWrite: update,
  conditionalRendering: conditionalRendering
});


/*
 * callback for standard mode
 */
function readStandardModeCallback(cpeParameters) {  
  if (typeof cpeParameters.Standard == 'undefined' || cpeParameters.Standard === null) {
    return null;
  }
  if (typeof cpeParameters.Standard.value == 'undefined' || cpeParameters.Standard.value === null) {
    log.info("Standard value not set. Most likely parameter not set as RELEVANT in device model");
    return null;
  }

  var parameter = {}; 
  parameter.writable = cpeParameters.Standard.writable;
  parameter.stale = cpeParameters.Standard.stale;
  parameter.value = cpeParameters.Standard.value;

  if(parameter.value == "b, g") {
    parameter.value = "Mixed 11b &amp; 11g";
  }
  if(parameter.value == "b, g, n") {
    parameter.value = "Mixed 11b, 11g &amp; 11n";
  }
  if(parameter.value == "n") {
    parameter.value = "11n Only";
  }
  if(parameter.value == "b") {
    parameter.value = "11b Only";
  }
  if(parameter.value == "g") {
    parameter.value = "11g Only";
  }

  parameter.dataType = {
    type: "ENUM",
    choice:[
      { systemName:"b", friendlyName: "11b Only" },
      { systemName:"g", friendlyName: "11g Only" },
      { systemName:"b, g", friendlyName: "Mixed 11b &amp; 11g" },
      { systemName:"n", friendlyName: "11n Only" },
      { systemName:"b, g, n", friendlyName: "Mixed 11b, 11g &amp; 11n" }
    ]
  };
  return parameter;
}

/*
 * callback for security mode
 */
function readSecurityModeCallback(cpeParameters) {
  if (typeof cpeParameters.BeaconType == 'undefined' || cpeParameters.BeaconType === null) {
    return null;
  }
  if (typeof cpeParameters.BeaconType.value == 'undefined' || cpeParameters.BeaconType.value === null) {
    log.info("BeaconType value not set. Most likely parameter not set as RELEVANT in device model");
    return null;
  }
  if (typeof cpeParameters.WPAEncryptionModes == 'undefined' || cpeParameters.WPAEncryptionModes === null) {
    return null;
  }
  if (typeof cpeParameters.WPAEncryptionModes.value == 'undefined' || cpeParameters.WPAEncryptionModes.value === null) {
    log.info("WPAEncryptionModes value not set. Most likely parameter not set as RELEVANT in device model");
    return null;
  }
  if (typeof cpeParameters.BasicAuthenticationMode == 'undefined' || cpeParameters.BasicAuthenticationMode === null) {
    return null;
  }
  if (typeof cpeParameters.BasicEncryptionModes == 'undefined' || cpeParameters.BasicEncryptionModes === null) {
    return null;
  }

  var security;
  if (cpeParameters.BasicEncryptionModes.value == "WEPEncryption") {
    security = "WEP-Open";
    if (cpeParameters.BasicAuthenticationMode.value == "SharedAuthentication") {
      security = "WEP-Shared";
    }
  } else {
    if (cpeParameters.BeaconType.value == "Basic") {
      security = "Disabled";      
    } else {
      if(cpeParameters.WPAAuthenticationMode.value == "EAPAuthentication") {
        security = "EAPAuthentication";
      } else {
        security = cpeParameters.WPAEncryptionModes.value;
      }
    }
  }

  log.info("--------------------- security = " + cpeParameters.WPAEncryptionModes.value);
  var parameter = {}; 
  parameter.writable = cpeParameters.BeaconType.writable;
  parameter.stale = cpeParameters.BeaconType.stale;
  parameter.value = security;
  parameter.disabled = false;
  parameter.dataType = {
    type: "ENUM",
    choice:[
      { systemName: "Disabled", friendlyName : "Disabled" },
      { systemName: "WEP-Open", friendlyName : "WEP-Open" },
      { systemName: "WEP-Shared", friendlyName : "WEP-Shared" },
      { systemName: "TKIPEncryption", friendlyName : "WPA-PSK(TKIP)" },
      { systemName: "AESEncryption", friendlyName : "WPA2-PSK(AES)" },
      { systemName: "TKIPandAESEncryption", friendlyName : "Mixed WPA/WPA2" },
      { systemName: "EAPAuthentication", friendlyName : "Enterprise (802.1x)" }
    ]
  };

  return parameter;
}

function update(cpeParameters) {

  log.info("CPE script parameters:");
  for(var name in scriptParameters) {
    log.info(" " + name + "=" + scriptParameters[name]);
  }

  for(name in scriptParameters) {
    var value = scriptParameters[name];
    switch (name){
    case "SSID": 
          cpeParameters.SSID.value = value;
          cpeParameters.SSID.updated = true;
          break;
    case "Channel": 
          if(value &lt; 0 || value &gt; 11)
             throw "Channel number invalid. Must be 1 - 11";
          cpeParameters.Channel.value = value;
          cpeParameters.Channel.updated = true;
          break;
    case "Enabled":
          cpeParameters.Enabled.value = value === "true" ? 1 : 0;
          cpeParameters.Enabled.updated = true;
          break;
    case "BroadcastSSID":
          cpeParameters.BroadcastSSID.value = value === "true" ? 1 : 0;
          cpeParameters.BroadcastSSID.updated = true;
          break;
    case "Standard":
          cpeParameters.Standard.value = value;
          cpeParameters.Standard.updated = true;
          break;
    case "SecurityMode":         
          if (value == "Disabled") {
            cpeParameters.BasicAuthenticationMode.value = "None";
            cpeParameters.BasicAuthenticationMode.updated = true;
            cpeParameters.BasicEncryptionModes.value = "None";
            cpeParameters.BasicEncryptionModes.updated = true;
            cpeParameters.BeaconType.value = "Basic";
            cpeParameters.BeaconType.updated = true;
          } else if(value == "WEP-Shared" || value == "WEP-Open") {
            if(typeof scriptParameters.CurrentPasswordIndex != 'undefined') {
              var PasswordIndex = parseInt(scriptParameters.CurrentPasswordIndex,10);
              if(PasswordIndex &lt; 1 &amp;&amp; PasswordIndex &gt; 4)
                throw "Key index must be between 1 and 4";
              cpeParameters.CurrentPasswordIndex.value = scriptParameters.CurrentPasswordIndex;
              cpeParameters.CurrentPasswordIndex.updated = true;
            } else {
              throw "Key index must be between 1 and 4";
            }

            if (typeof scriptParameters.Password1 != 'undefined' &amp;&amp; scriptParameters.Password1 != null) {
              if(scriptParameters.Password1.length !== 0 &amp;&amp; scriptParameters.Password1.length != 13 &amp;&amp; scriptParameters.Password1.length != 5)
                throw "Password1 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password1.value = scriptParameters.Password1;
              cpeParameters.Password1.updated = true;
            }
            if (typeof scriptParameters.Password2 != 'undefined' &amp;&amp; scriptParameters.Password2 != null) {
              if(scriptParameters.Password2.length !== 0 &amp;&amp; scriptParameters.Password2.length != 13 &amp;&amp; scriptParameters.Password2.length != 5)
                throw "Password2 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password2.value = scriptParameters.Password2;
              cpeParameters.Password2.updated = true;
            }
            if (typeof scriptParameters.Password3 != 'undefined' &amp;&amp; scriptParameters.Password3 != null) {
              if(scriptParameters.Password3.length !== 0 &amp;&amp; scriptParameters.Password3.length != 13 &amp;&amp; scriptParameters.Password3.length != 5)
                throw "Password3 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password3.value = scriptParameters.Password3;
              cpeParameters.Password3.updated = true;
            }
            if (typeof scriptParameters.Password4 != 'undefined' &amp;&amp; scriptParameters.Password4 != null) {
              if(scriptParameters.Password4.length !== 0 &amp;&amp; scriptParameters.Password4.length != 13 &amp;&amp; scriptParameters.Password4.length != 5)
                throw "Password4 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password4.value = scriptParameters.Password4;
              cpeParameters.Password4.updated = true;
            }

            if(value == "WEP-Shared") {
              cpeParameters.BasicAuthenticationMode.value = "SharedAuthentication";
              cpeParameters.BasicAuthenticationMode.updated = true;
            } else {
              cpeParameters.BasicAuthenticationMode.value = "None";
              cpeParameters.BasicAuthenticationMode.updated = true;
            }
            cpeParameters.BasicEncryptionModes.value = "WEPEncryption";
            cpeParameters.BasicEncryptionModes.updated = true;
            cpeParameters.BeaconType.value = "Basic";
            cpeParameters.BeaconType.updated = true;
          } else if(value == "EAPAuthentication") {
            cpeParameters.BeaconType.value = "WPA";
            cpeParameters.BeaconType.updated = true;
            cpeParameters.WPAAuthenticationMode.value = "EAPAuthentication";
            cpeParameters.WPAAuthenticationMode.updated = true;
            cpeParameters.WPAEncryptionModes.value = "TKIPandAESEncryption";
            cpeParameters.WPAEncryptionModes.updated = true;
            cpeParameters.BasicAuthenticationMode.value = "None";
            cpeParameters.BasicAuthenticationMode.updated = true;
            cpeParameters.BasicEncryptionModes.value = "None";
            cpeParameters.BasicEncryptionModes.updated = true;
          } else if(value == "TKIPEncryption" || value == "AESEncryption" || value == "TKIPandAESEncryption") {            
            cpeParameters.BeaconType.value = "WPA";
            cpeParameters.BeaconType.updated = true;
            cpeParameters.WPAAuthenticationMode.value = "PSKAuthentication";
            cpeParameters.WPAAuthenticationMode.updated = true;
            cpeParameters.WPAEncryptionModes.value = value;
            cpeParameters.WPAEncryptionModes.updated = true;
            cpeParameters.BasicAuthenticationMode.value = "None";
            cpeParameters.BasicAuthenticationMode.updated = true;
            cpeParameters.BasicEncryptionModes.value = "None";
            cpeParameters.BasicEncryptionModes.updated = true;

            if (typeof scriptParameters.Password != 'undefined' &amp;&amp; scriptParameters.Password !== null) {
              if(scriptParameters.Password.length &lt; 8)
                throw "Password length invalid. Must be 8-63 ASCII characters";
              cpeParameters.Password.value = scriptParameters.Password;
              cpeParameters.Password.updated = true;
            }
          }
          break;
       default : 
          break;
    }
  }
  return cpeParameters;
}

response;
</javaScriptCode>
        </scriptDefinition>
    </deviceServiceConfigurations>
    <deviceServiceConfigurations name="WiFi 1">
        <scriptDefinition name="TP-Link_IGD_LAB: WiFi 1" purpose="Device service configuration" tags="null" scriptParameters="[]">
            <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var channelDataType = {
  type: "ENUM", 
  choice:[
    { systemName: "0", friendlyName: "auto" },
    { systemName: "1", friendlyName: "1" },
    { systemName: "2", friendlyName: "2" },
    { systemName: "3", friendlyName: "3" },
    { systemName: "4", friendlyName: "4" },
    { systemName: "5", friendlyName: "5" },
    { systemName: "6", friendlyName: "6" },
    { systemName: "7", friendlyName: "7" },
    { systemName: "8", friendlyName: "8" },
    { systemName: "9", friendlyName: "9" },
    { systemName: "10", friendlyName: "10" },
    { systemName: "11", friendlyName: "11" }
  ]
};

var conditionalRendering = [
  {
    group: "WEP-Open",
    dependsOnParameter: "SecurityMode",
    showOnValue: ["WEP-Open"]
  },
  {
    group: "WEP-Shared",
    dependsOnParameter: "SecurityMode",
    showOnValue: ["WEP-Shared"]
  },
  {
    group: "WPA",
    dependsOnParameter: "SecurityMode",
    showOnValue: ["TKIPEncryption", "AESEncryption", "TKIPandAESEncryption"]
  }
];

var data = {
  label: "WiFi",
  parameters: [
    { label: "SSID", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.SSID" },
    { label: "Enabled", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Enable" },
    { label: "Broadcast SSID", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.BeaconAdvertisementEnabled" },
    { label: "Channel", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel", dataType: channelDataType },
    { label: "Current Password Index", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKeyIndex", groups: ["WEP-Open", "WEP-Shared"] },
    { label: "Password 1", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.1.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    { label: "Password 2", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.2.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    { label: "Password 3", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.3.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    { label: "Password 4", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.4.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    { label: "Password", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.PreSharedKey.1.PreSharedKey", group: "WPA" },
    { label: "WPAA uthentication Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WPAAuthenticationMode", internalOnly: true },
    { label: "WPA Encryption Modes", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WPAEncryptionModes", internalOnly: true },
    { label: "Basic Authentication Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.BasicAuthenticationMode", internalOnly: true },
    { label: "Basic Encryption Modes", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.BasicEncryptionModes", internalOnly: true },
    { label: "Beacon Type", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.BeaconType", internalOnly: true },
    { label: "Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Standard", internalOnly: true },
    { label: "Mode", description: "Standard Mode", readCallback: readStandardModeCallback, writable: false },
    { label: "Security Mode", description: "Security Mode", readCallback: readSecurityModeCallback }
  ]
};

var response = dsc.createResponse({
  data: data,
  scriptParameters: scriptParameters,
  customWrite: update,
  conditionalRendering: conditionalRendering
});


/*
 * callback for standard mode
 */
function readStandardModeCallback(cpeParameters) {  
  if (typeof cpeParameters.Standard == 'undefined' || cpeParameters.Standard === null) {
    return null;
  }
  if (typeof cpeParameters.Standard.value == 'undefined' || cpeParameters.Standard.value === null) {
    log.info("Standard value not set. Most likely parameter not set as RELEVANT in device model");
    return null;
  }

  var parameter = {}; 
  parameter.writable = cpeParameters.Standard.writable;
  parameter.stale = cpeParameters.Standard.stale;
  parameter.value = cpeParameters.Standard.value;

  if(parameter.value == "b, g") {
    parameter.value = "Mixed 11b &amp; 11g";
  }
  if(parameter.value == "b, g, n") {
    parameter.value = "Mixed 11b, 11g &amp; 11n";
  }
  if(parameter.value == "n") {
    parameter.value = "11n Only";
  }
  if(parameter.value == "b") {
    parameter.value = "11b Only";
  }
  if(parameter.value == "g") {
    parameter.value = "11g Only";
  }

  parameter.dataType = {
    type: "ENUM",
    choice:[
      { systemName:"b", friendlyName: "11b Only" },
      { systemName:"g", friendlyName: "11g Only" },
      { systemName:"b, g", friendlyName: "Mixed 11b &amp; 11g" },
      { systemName:"n", friendlyName: "11n Only" },
      { systemName:"b, g, n", friendlyName: "Mixed 11b, 11g &amp; 11n" }
    ]
  };
  return parameter;
}

/*
 * callback for security mode
 */
function readSecurityModeCallback(cpeParameters) {
  if (typeof cpeParameters.BeaconType == 'undefined' || cpeParameters.BeaconType === null) {
    return null;
  }
  if (typeof cpeParameters.BeaconType.value == 'undefined' || cpeParameters.BeaconType.value === null) {
    log.info("BeaconType value not set. Most likely parameter not set as RELEVANT in device model");
    return null;
  }
  if (typeof cpeParameters.WPAEncryptionModes == 'undefined' || cpeParameters.WPAEncryptionModes === null) {
    return null;
  }
  if (typeof cpeParameters.WPAEncryptionModes.value == 'undefined' || cpeParameters.WPAEncryptionModes.value === null) {
    log.info("WPAEncryptionModes value not set. Most likely parameter not set as RELEVANT in device model");
    return null;
  }
  if (typeof cpeParameters.BasicAuthenticationMode == 'undefined' || cpeParameters.BasicAuthenticationMode === null) {
    return null;
  }
  if (typeof cpeParameters.BasicEncryptionModes == 'undefined' || cpeParameters.BasicEncryptionModes === null) {
    return null;
  }

  var security;
  if (cpeParameters.BasicEncryptionModes.value == "WEPEncryption") {
    security = "WEP-Open";
    if (cpeParameters.BasicAuthenticationMode.value == "SharedAuthentication") {
      security = "WEP-Shared";
    }
  } else {
    if (cpeParameters.BeaconType.value == "Basic") {
      security = "Disabled";      
    } else {
      if(cpeParameters.WPAAuthenticationMode.value == "EAPAuthentication") {
        security = "EAPAuthentication";
      } else {
        security = cpeParameters.WPAEncryptionModes.value;
      }
    }
  }

  log.info("--------------------- security = " + cpeParameters.WPAEncryptionModes.value);
  var parameter = {}; 
  parameter.writable = cpeParameters.BeaconType.writable;
  parameter.stale = cpeParameters.BeaconType.stale;
  parameter.value = security;
  parameter.disabled = false;
  parameter.dataType = {
    type: "ENUM",
    choice:[
      { systemName: "Disabled", friendlyName : "Disabled" },
      { systemName: "WEP-Open", friendlyName : "WEP-Open" },
      { systemName: "WEP-Shared", friendlyName : "WEP-Shared" },
      { systemName: "TKIPEncryption", friendlyName : "WPA-PSK(TKIP)" },
      { systemName: "AESEncryption", friendlyName : "WPA2-PSK(AES)" },
      { systemName: "TKIPandAESEncryption", friendlyName : "Mixed WPA/WPA2" },
      { systemName: "EAPAuthentication", friendlyName : "Enterprise (802.1x)" }
    ]
  };

  return parameter;
}

function update(cpeParameters) {

  log.info("CPE script parameters:");
  for(var name in scriptParameters) {
    log.info(" " + name + "=" + scriptParameters[name]);
  }

  for(name in scriptParameters) {
    var value = scriptParameters[name];
    switch (name){
    case "SSID": 
          cpeParameters.SSID.value = value;
          cpeParameters.SSID.updated = true;
          break;
    case "Channel": 
          if(value &lt; 0 || value &gt; 11)
             throw "Channel number invalid. Must be 1 - 11";
          cpeParameters.Channel.value = value;
          cpeParameters.Channel.updated = true;
          break;
    case "Enabled":
          cpeParameters.Enabled.value = value === "true" ? 1 : 0;
          cpeParameters.Enabled.updated = true;
          break;
    case "BroadcastSSID":
          cpeParameters.BroadcastSSID.value = value === "true" ? 1 : 0;
          cpeParameters.BroadcastSSID.updated = true;
          break;
    case "Standard":
          cpeParameters.Standard.value = value;
          cpeParameters.Standard.updated = true;
          break;
    case "SecurityMode":         
          if (value == "Disabled") {
            cpeParameters.BasicAuthenticationMode.value = "None";
            cpeParameters.BasicAuthenticationMode.updated = true;
            cpeParameters.BasicEncryptionModes.value = "None";
            cpeParameters.BasicEncryptionModes.updated = true;
            cpeParameters.BeaconType.value = "Basic";
            cpeParameters.BeaconType.updated = true;
          } else if(value == "WEP-Shared" || value == "WEP-Open") {
            if(typeof scriptParameters.CurrentPasswordIndex != 'undefined') {
              var PasswordIndex = parseInt(scriptParameters.CurrentPasswordIndex,10);
              if(PasswordIndex &lt; 1 &amp;&amp; PasswordIndex &gt; 4)
                throw "Key index must be between 1 and 4";
              cpeParameters.CurrentPasswordIndex.value = scriptParameters.CurrentPasswordIndex;
              cpeParameters.CurrentPasswordIndex.updated = true;
            } else {
              throw "Key index must be between 1 and 4";
            }

            if (typeof scriptParameters.Password1 != 'undefined' &amp;&amp; scriptParameters.Password1 != null) {
              if(scriptParameters.Password1.length !== 0 &amp;&amp; scriptParameters.Password1.length != 13 &amp;&amp; scriptParameters.Password1.length != 5)
                throw "Password1 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password1.value = scriptParameters.Password1;
              cpeParameters.Password1.updated = true;
            }
            if (typeof scriptParameters.Password2 != 'undefined' &amp;&amp; scriptParameters.Password2 != null) {
              if(scriptParameters.Password2.length !== 0 &amp;&amp; scriptParameters.Password2.length != 13 &amp;&amp; scriptParameters.Password2.length != 5)
                throw "Password2 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password2.value = scriptParameters.Password2;
              cpeParameters.Password2.updated = true;
            }
            if (typeof scriptParameters.Password3 != 'undefined' &amp;&amp; scriptParameters.Password3 != null) {
              if(scriptParameters.Password3.length !== 0 &amp;&amp; scriptParameters.Password3.length != 13 &amp;&amp; scriptParameters.Password3.length != 5)
                throw "Password3 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password3.value = scriptParameters.Password3;
              cpeParameters.Password3.updated = true;
            }
            if (typeof scriptParameters.Password4 != 'undefined' &amp;&amp; scriptParameters.Password4 != null) {
              if(scriptParameters.Password4.length !== 0 &amp;&amp; scriptParameters.Password4.length != 13 &amp;&amp; scriptParameters.Password4.length != 5)
                throw "Password4 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password4.value = scriptParameters.Password4;
              cpeParameters.Password4.updated = true;
            }

            if(value == "WEP-Shared") {
              cpeParameters.BasicAuthenticationMode.value = "SharedAuthentication";
              cpeParameters.BasicAuthenticationMode.updated = true;
            } else {
              cpeParameters.BasicAuthenticationMode.value = "None";
              cpeParameters.BasicAuthenticationMode.updated = true;
            }
            cpeParameters.BasicEncryptionModes.value = "WEPEncryption";
            cpeParameters.BasicEncryptionModes.updated = true;
            cpeParameters.BeaconType.value = "Basic";
            cpeParameters.BeaconType.updated = true;
          } else if(value == "EAPAuthentication") {
            cpeParameters.BeaconType.value = "WPA";
            cpeParameters.BeaconType.updated = true;
            cpeParameters.WPAAuthenticationMode.value = "EAPAuthentication";
            cpeParameters.WPAAuthenticationMode.updated = true;
            cpeParameters.WPAEncryptionModes.value = "TKIPandAESEncryption";
            cpeParameters.WPAEncryptionModes.updated = true;
            cpeParameters.BasicAuthenticationMode.value = "None";
            cpeParameters.BasicAuthenticationMode.updated = true;
            cpeParameters.BasicEncryptionModes.value = "None";
            cpeParameters.BasicEncryptionModes.updated = true;
          } else if(value == "TKIPEncryption" || value == "AESEncryption" || value == "TKIPandAESEncryption") {            
            cpeParameters.BeaconType.value = "WPA";
            cpeParameters.BeaconType.updated = true;
            cpeParameters.WPAAuthenticationMode.value = "PSKAuthentication";
            cpeParameters.WPAAuthenticationMode.updated = true;
            cpeParameters.WPAEncryptionModes.value = value;
            cpeParameters.WPAEncryptionModes.updated = true;
            cpeParameters.BasicAuthenticationMode.value = "None";
            cpeParameters.BasicAuthenticationMode.updated = true;
            cpeParameters.BasicEncryptionModes.value = "None";
            cpeParameters.BasicEncryptionModes.updated = true;

            if (typeof scriptParameters.Password != 'undefined' &amp;&amp; scriptParameters.Password !== null) {
              if(scriptParameters.Password.length &lt; 8)
                throw "Password length invalid. Must be 8-63 ASCII characters";
              cpeParameters.Password.value = scriptParameters.Password;
              cpeParameters.Password.updated = true;
            }
          }
          break;
       default : 
          break;
    }
  }
  return cpeParameters;
}

response;
</javaScriptCode>
        </scriptDefinition>
    </deviceServiceConfigurations>
    <deviceServiceConfigurations name="WiFi 5 TP">
        <scriptDefinition name="TP-Link_IGD_CABO:WiFi 5 TP" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
            <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var channelDataType = {
  type: "ENUM", 
  choice:[
    //{ systemName: "0", friendlyName: "auto" },
    { systemName: "0", friendlyName: "auto" },
    { systemName: "36", friendlyName: "36" },
    { systemName: "40", friendlyName: "40" },
    { systemName: "44", friendlyName: "44" },
    { systemName: "48", friendlyName: "48" },
    { systemName: "52", friendlyName: "52" },
    { systemName: "60", friendlyName: "60" },
    { systemName: "64", friendlyName: "64" },
    { systemName: "100", friendlyName: "100" },
    { systemName: "104", friendlyName: "104" },
    { systemName: "108", friendlyName: "108" },
    { systemName: "112", friendlyName: "112" },
    { systemName: "116", friendlyName: "116" },
    { systemName: "120", friendlyName: "120" },
    { systemName: "124", friendlyName: "124" },
    { systemName: "128", friendlyName: "128" },
    { systemName: "149", friendlyName: "149" },
    { systemName: "153", friendlyName: "153" },
    { systemName: "157", friendlyName: "157" },
    { systemName: "161", friendlyName: "161" }
  ]
};

var Auto = {
  type: "BOOLEAN", 
  choice:[
    { systemName: "1", friendlyName: "Enabled" },
    { systemName: "0", friendlyName: "Disabled" }

  ]
};

var conditionalRendering = [
  {
    group: "WEP-Open",
    dependsOnParameter: "SecurityMode",
    showOnValue: ["WEP-Open"]
  },
  {
    group: "WEP-Shared",
    dependsOnParameter: "SecurityMode",
    showOnValue: ["WEP-Shared"]
  },
  {
    group: "WPA",
    dependsOnParameter: "SecurityMode",
    showOnValue: ["TKIPEncryption", "AESEncryption", "TKIPandAESEncryption"]
  }
];

var data = {
  label: "WiFi",
  parameters: [
    { label: "SSID", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.SSID" },
    { label: "Enabled", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Enable" },
    //{ label: "AutoChannel", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.AutoChannelEnable", dataType: Auto},
    { label: "Channel", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel", dataType: channelDataType },
    { label: "Password", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.X_TP_PreSharedKey", group: "WPA" },
    { label: "WPA Authentication Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.WPAAuthenticationMode", internalOnly: true },
    { label: "WPA Encryption Modes", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.WPAEncryptionModes", internalOnly: true },
    { label: "Basic Authentication Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.BasicAuthenticationMode", internalOnly: true },
    { label: "Basic Encryption Modes", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.BasicEncryptionModes", internalOnly: true },
    { label: "Beacon Type", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.BeaconType", internalOnly: true },
    { label: "Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Standard", internalOnly: true }
  ]
};

var response = dsc.createResponse({
  data: data,
  scriptParameters: scriptParameters,
  customWrite: update,
  conditionalRendering: conditionalRendering
});


/*
 * callback for standard mode
 */
function readStandardModeCallback(cpeParameters) {  
  if (typeof cpeParameters.Standard == 'undefined' || cpeParameters.Standard === null) {
    return null;
  }
  if (typeof cpeParameters.Standard.value == 'undefined' || cpeParameters.Standard.value === null) {
    log.info("Standard value not set. Most likely parameter not set as RELEVANT in device model");
    return null;
  }

  var parameter = {}; 
  parameter.writable = cpeParameters.Standard.writable;
  parameter.stale = cpeParameters.Standard.stale;
  parameter.value = cpeParameters.Standard.value;

  if(parameter.value == "b, g") {
    parameter.value = "Mixed 11b &amp; 11g";
  }
  if(parameter.value == "b, g, n") {
    parameter.value = "Mixed 11b, 11g &amp; 11n";
  }
  if(parameter.value == "n") {
    parameter.value = "11n Only";
  }
  if(parameter.value == "b") {
    parameter.value = "11b Only";
  }
  if(parameter.value == "g") {
    parameter.value = "11g Only";
  }

  parameter.dataType = {
    type: "ENUM",
    choice:[
      { systemName:"b", friendlyName: "11b Only" },
      { systemName:"g", friendlyName: "11g Only" },
      { systemName:"b, g", friendlyName: "Mixed 11b &amp; 11g" },
      { systemName:"n", friendlyName: "11n Only" },
      { systemName:"b, g, n", friendlyName: "Mixed 11b, 11g &amp; 11n" }
    ]
  };
  return parameter;
}

/*
 * callback for security mode
 */
function readSecurityModeCallback(cpeParameters) {
  if (typeof cpeParameters.BeaconType == 'undefined' || cpeParameters.BeaconType === null) {
    return null;
  }
  if (typeof cpeParameters.BeaconType.value == 'undefined' || cpeParameters.BeaconType.value === null) {
    log.info("BeaconType value not set. Most likely parameter not set as RELEVANT in device model");
    return null;
  }
  if (typeof cpeParameters.WPAEncryptionModes == 'undefined' || cpeParameters.WPAEncryptionModes === null) {
    return null;
  }
  if (typeof cpeParameters.WPAEncryptionModes.value == 'undefined' || cpeParameters.WPAEncryptionModes.value === null) {
    log.info("WPAEncryptionModes value not set. Most likely parameter not set as RELEVANT in device model");
    return null;
  }
  if (typeof cpeParameters.BasicAuthenticationMode == 'undefined' || cpeParameters.BasicAuthenticationMode === null) {
    return null;
  }
  if (typeof cpeParameters.BasicEncryptionModes == 'undefined' || cpeParameters.BasicEncryptionModes === null) {
    return null;
  }

  var security;
  if (cpeParameters.BasicEncryptionModes.value == "WEPEncryption") {
    security = "WEP-Open";
    if (cpeParameters.BasicAuthenticationMode.value == "SharedAuthentication") {
      security = "WEP-Shared";
    }
  } else {
    if (cpeParameters.BeaconType.value == "Basic") {
      security = "Disabled";      
    } else {
      if(cpeParameters.WPAAuthenticationMode.value == "EAPAuthentication") {
        security = "EAPAuthentication";
      } else {
        security = cpeParameters.WPAEncryptionModes.value;
      }
    }
  }

  log.info("--------------------- security = " + cpeParameters.WPAEncryptionModes.value);
  var parameter = {}; 
  parameter.writable = cpeParameters.BeaconType.writable;
  parameter.stale = cpeParameters.BeaconType.stale;
  parameter.value = security;
  parameter.disabled = false;
  parameter.dataType = {
    type: "ENUM",
    choice:[
      { systemName: "Disabled", friendlyName : "Disabled" },
      { systemName: "WEP-Open", friendlyName : "WEP-Open" },
      { systemName: "WEP-Shared", friendlyName : "WEP-Shared" },
      { systemName: "TKIPEncryption", friendlyName : "WPA-PSK(TKIP)" },
      { systemName: "AESEncryption", friendlyName : "WPA2-PSK(AES)" },
      { systemName: "TKIPandAESEncryption", friendlyName : "Mixed WPA/WPA2" },
      { systemName: "EAPAuthentication", friendlyName : "Enterprise (802.1x)" }
    ]
  };

  return parameter;
}

function update(cpeParameters) {

  log.info("CPE script parameters:");
  for(var name in scriptParameters) {
    log.info(" " + name + "=" + scriptParameters[name]);
  }

  for(name in scriptParameters) {
    var value = scriptParameters[name];
    switch (name){
    case "SSID": 
          cpeParameters.SSID.value = value;
          cpeParameters.SSID.updated = true;
          break;
    case "Channel": 
          if(value &lt; 0 || value &gt; 200)
             throw "Channel number invalid. Must be 1 - 11";
          cpeParameters.Channel.value = value;
          cpeParameters.Channel.updated = true;
          break;
    case "Enabled":
          cpeParameters.Enabled.value = value === "true" ? 1 : 0;
          cpeParameters.Enabled.updated = true;
          break;

   

    case "AutoChannel": 
          cpeParameters.AutoChannel.value = value;
          cpeParameters.AutoChannel.updated = true;
          break;
        
        
    case "Standard":
          cpeParameters.Standard.value = value;
          cpeParameters.Standard.updated = true;
          break;
    case "SecurityMode":         
          if (value == "Disabled") {
            cpeParameters.BasicAuthenticationMode.value = "None";
            cpeParameters.BasicAuthenticationMode.updated = true;
            cpeParameters.BasicEncryptionModes.value = "None";
            cpeParameters.BasicEncryptionModes.updated = true;
            cpeParameters.BeaconType.value = "Basic";
            cpeParameters.BeaconType.updated = true;
          } else if(value == "WEP-Shared" || value == "WEP-Open") {
            if(typeof scriptParameters.CurrentPasswordIndex != 'undefined') {
              var PasswordIndex = parseInt(scriptParameters.CurrentPasswordIndex,10);
              if(PasswordIndex &lt; 1 &amp;&amp; PasswordIndex &gt; 4)
                throw "Key index must be between 1 and 4";
              cpeParameters.CurrentPasswordIndex.value = scriptParameters.CurrentPasswordIndex;
              cpeParameters.CurrentPasswordIndex.updated = true;
            } else {
              throw "Key index must be between 1 and 4";
            }

            if (typeof scriptParameters.Password1 != 'undefined' &amp;&amp; scriptParameters.Password1 != null) {
              if(scriptParameters.Password1.length !== 0 &amp;&amp; scriptParameters.Password1.length != 13 &amp;&amp; scriptParameters.Password1.length != 5)
                throw "Password1 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password1.value = scriptParameters.Password1;
              cpeParameters.Password1.updated = true;
            }
            if (typeof scriptParameters.Password2 != 'undefined' &amp;&amp; scriptParameters.Password2 != null) {
              if(scriptParameters.Password2.length !== 0 &amp;&amp; scriptParameters.Password2.length != 13 &amp;&amp; scriptParameters.Password2.length != 5)
                throw "Password2 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password2.value = scriptParameters.Password2;
              cpeParameters.Password2.updated = true;
            }
            if (typeof scriptParameters.Password3 != 'undefined' &amp;&amp; scriptParameters.Password3 != null) {
              if(scriptParameters.Password3.length !== 0 &amp;&amp; scriptParameters.Password3.length != 13 &amp;&amp; scriptParameters.Password3.length != 5)
                throw "Password3 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password3.value = scriptParameters.Password3;
              cpeParameters.Password3.updated = true;
            }
            if (typeof scriptParameters.Password4 != 'undefined' &amp;&amp; scriptParameters.Password4 != null) {
              if(scriptParameters.Password4.length !== 0 &amp;&amp; scriptParameters.Password4.length != 13 &amp;&amp; scriptParameters.Password4.length != 5)
                throw "Password4 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password4.value = scriptParameters.Password4;
              cpeParameters.Password4.updated = true;
            }

            if(value == "WEP-Shared") {
              cpeParameters.BasicAuthenticationMode.value = "SharedAuthentication";
              cpeParameters.BasicAuthenticationMode.updated = true;
            } else {
              cpeParameters.BasicAuthenticationMode.value = "None";
              cpeParameters.BasicAuthenticationMode.updated = true;
            }
            cpeParameters.BasicEncryptionModes.value = "WEPEncryption";
            cpeParameters.BasicEncryptionModes.updated = true;
            cpeParameters.BeaconType.value = "Basic";
            cpeParameters.BeaconType.updated = true;
          } else if(value == "EAPAuthentication") {
            cpeParameters.BeaconType.value = "WPA";
            cpeParameters.BeaconType.updated = true;
            cpeParameters.WPAAuthenticationMode.value = "EAPAuthentication";
            cpeParameters.WPAAuthenticationMode.updated = true;
            cpeParameters.WPAEncryptionModes.value = "TKIPandAESEncryption";
            cpeParameters.WPAEncryptionModes.updated = true;
            cpeParameters.BasicAuthenticationMode.value = "None";
            cpeParameters.BasicAuthenticationMode.updated = true;
            cpeParameters.BasicEncryptionModes.value = "None";
            cpeParameters.BasicEncryptionModes.updated = true;
          } else if(value == "TKIPEncryption" || value == "AESEncryption" || value == "TKIPandAESEncryption") {            
            cpeParameters.BeaconType.value = "WPA";
            cpeParameters.BeaconType.updated = true;
            cpeParameters.WPAAuthenticationMode.value = "PSKAuthentication";
            cpeParameters.WPAAuthenticationMode.updated = true;
            cpeParameters.WPAEncryptionModes.value = value;
            cpeParameters.WPAEncryptionModes.updated = true;
            cpeParameters.BasicAuthenticationMode.value = "None";
            cpeParameters.BasicAuthenticationMode.updated = true;
            cpeParameters.BasicEncryptionModes.value = "None";
            cpeParameters.BasicEncryptionModes.updated = true;

            if (typeof scriptParameters.Password != 'undefined' &amp;&amp; scriptParameters.Password !== null) {
              if(scriptParameters.Password.length &lt; 8)
                throw "Password length invalid. Must be 8-63 ASCII characters";
              cpeParameters.Password.value = scriptParameters.Password;
              cpeParameters.Password.updated = true;
            }
          }
          break;
       default : 
          break;
    }
  }
  return cpeParameters;
}

response;
</javaScriptCode>
        </scriptDefinition>
    </deviceServiceConfigurations>
    <deviceServiceConfigurations name="TR-69 Config">
        <scriptDefinition name="TP-Link_IGD_LAB: TR-69 Config" purpose="Device service configuration" tags="null" scriptParameters="[]">
            <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var data = {
  label: "TR69 Config",
  parameters: [
    { label: "Connection Request Username", cpeParameterName:"InternetGatewayDevice.ManagementServer.ConnectionRequestUsername" },
    { label: "Connection Request Password", cpeParameterName:"InternetGatewayDevice.ManagementServer.ConnectionRequestPassword" },
    { label: "Connection Request URL", cpeParameterName:"InternetGatewayDevice.ManagementServer.ConnectionRequestURL", readOnly: true },
    { label: "Periodic Inform Interval", cpeParameterName:"InternetGatewayDevice.ManagementServer.PeriodicInformInterval" },
    { label: "CPE Username", cpeParameterName:"InternetGatewayDevice.ManagementServer.Username" },
    { label: "CPE Password", cpeParameterName:"InternetGatewayDevice.ManagementServer.Password" }
  ]
};

var response = dsc.createResponse({
    data: data,
    scriptParameters: scriptParameters
});

response;
</javaScriptCode>
        </scriptDefinition>
    </deviceServiceConfigurations>
    <deviceServiceConfigurations name="Device Log">
        <scriptDefinition name="TP-Link_IGD_LAB: Device Log" purpose="Device service configuration" tags="null" scriptParameters="[]">
            <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var deviceId = scriptParameters.deviceId;
var response = dsc.getDeviceParameterLogs(deviceId);

response;
</javaScriptCode>
        </scriptDefinition>
    </deviceServiceConfigurations>
    <deviceServiceConfigurations name="WiFi 2.4 TP">
        <scriptDefinition name="TP-Link_IGD_CABO:WiFi 2.4 TP" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
            <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var channelDataType = {
  type: "ENUM", 
  choice:[
    { systemName: "0", friendlyName: "auto" },
    { systemName: "1", friendlyName: "1" },
    { systemName: "2", friendlyName: "2" },
    { systemName: "3", friendlyName: "3" },
    { systemName: "4", friendlyName: "4" },
    { systemName: "5", friendlyName: "5" },
    { systemName: "6", friendlyName: "6" },
    { systemName: "7", friendlyName: "7" },
    { systemName: "8", friendlyName: "8" },
    { systemName: "9", friendlyName: "9" },
    { systemName: "10", friendlyName: "10" },
    { systemName: "11", friendlyName: "11" },
    { systemName: "13", friendlyName: "13" }
  ]
};


var Auto = {
  type: "ENUM", 
  choice:[
    { systemName: "1", friendlyName: "Enabled" },
    { systemName: "0", friendlyName: "Disabled" }

  ]
};


var conditionalRendering = [
  {
    group: "WEP-Open",
    dependsOnParameter: "SecurityMode",
    showOnValue: ["WEP-Open"]
  },
  {
    group: "WEP-Shared",
    dependsOnParameter: "SecurityMode",
    showOnValue: ["WEP-Shared"]
  },
  {
    group: "WPA",
    dependsOnParameter: "SecurityMode",
    showOnValue: ["TKIPEncryption", "AESEncryption", "TKIPandAESEncryption"]
  }
];

var data = {
  label: "WiFi",
  parameters: [
    { label: "SSID", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.SSID" },
    { label: "Enabled", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Enable" },
    //{ label: "AutoChannel", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.AutoChannelEnable", dataType: Auto},
    { label: "Channel", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel", dataType: channelDataType },
    //{ label: "Auto Channel Refresh Period", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.X_ALU-COM_AutoChannelRefreshPeriod" },
    //{ label: "Current Password Index", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKeyIndex", groups: ["WEP-Open", "WEP-Shared"] },
    //{ label: "Password 1", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.1.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    //{ label: "Password 2", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.2.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    //{ label: "Password 3", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.3.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    //{ label: "Password 4", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.4.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    { label: "Password", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.X_TP_PreSharedKey", group: "WPA" }
   // { label: "WPAA uthentication Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WPAAuthenticationMode", internalOnly: true },
    //{ label: "WPA Encryption Modes", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WPAEncryptionModes", internalOnly: true },
   // { label: "Basic Authentication Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.BasicAuthenticationMode", internalOnly: true },
   // { label: "Basic Encryption Modes", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.BasicEncryptionModes", internalOnly: true },
   // { label: "Beacon Type", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.BeaconType", internalOnly: true },
    //{ label: "Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Standard", internalOnly: true },
    //{ label: "Mode", description: "Standard Mode", readCallback: readStandardModeCallback, writable: false },
    //{ label: "Security Mode", description: "Security Mode", readCallback: readSecurityModeCallback }
  ]
};

var response = dsc.createResponse({
  data: data,
  scriptParameters: scriptParameters,
  customWrite: update,
  conditionalRendering: conditionalRendering
});


/*
 * callback for standard mode
 */
function readStandardModeCallback(cpeParameters) {  
  if (typeof cpeParameters.Standard == 'undefined' || cpeParameters.Standard === null) {
    return null;
  }
  if (typeof cpeParameters.Standard.value == 'undefined' || cpeParameters.Standard.value === null) {
    log.info("Standard value not set. Most likely parameter not set as RELEVANT in device model");
    return null;
  }

  var parameter = {}; 
  parameter.writable = cpeParameters.Standard.writable;
  parameter.stale = cpeParameters.Standard.stale;
  parameter.value = cpeParameters.Standard.value;

  if(parameter.value == "b, g") {
    parameter.value = "Mixed 11b &amp; 11g";
  }
  if(parameter.value == "b, g, n") {
    parameter.value = "Mixed 11b, 11g &amp; 11n";
  }
  if(parameter.value == "n") {
    parameter.value = "11n Only";
  }
  if(parameter.value == "b") {
    parameter.value = "11b Only";
  }
  if(parameter.value == "g") {
    parameter.value = "11g Only";
  }

  parameter.dataType = {
    type: "ENUM",
    choice:[
      { systemName:"b", friendlyName: "11b Only" },
      { systemName:"g", friendlyName: "11g Only" },
      { systemName:"b, g", friendlyName: "Mixed 11b &amp; 11g" },
      { systemName:"n", friendlyName: "11n Only" },
      { systemName:"b, g, n", friendlyName: "Mixed 11b, 11g &amp; 11n" }
    ]
  };
  return parameter;
}

/*
 * callback for security mode
 */
function readSecurityModeCallback(cpeParameters) {
  if (typeof cpeParameters.BeaconType == 'undefined' || cpeParameters.BeaconType === null) {
    return null;
  }
  if (typeof cpeParameters.BeaconType.value == 'undefined' || cpeParameters.BeaconType.value === null) {
    log.info("BeaconType value not set. Most likely parameter not set as RELEVANT in device model");
    return null;
  }
  if (typeof cpeParameters.WPAEncryptionModes == 'undefined' || cpeParameters.WPAEncryptionModes === null) {
    return null;
  }
  if (typeof cpeParameters.WPAEncryptionModes.value == 'undefined' || cpeParameters.WPAEncryptionModes.value === null) {
    log.info("WPAEncryptionModes value not set. Most likely parameter not set as RELEVANT in device model");
    return null;
  }
  if (typeof cpeParameters.BasicAuthenticationMode == 'undefined' || cpeParameters.BasicAuthenticationMode === null) {
    return null;
  }
  if (typeof cpeParameters.BasicEncryptionModes == 'undefined' || cpeParameters.BasicEncryptionModes === null) {
    return null;
  }

  var security;
  if (cpeParameters.BasicEncryptionModes.value == "WEPEncryption") {
    security = "WEP-Open";
    if (cpeParameters.BasicAuthenticationMode.value == "SharedAuthentication") {
      security = "WEP-Shared";
    }
  } else {
    if (cpeParameters.BeaconType.value == "Basic") {
      security = "Disabled";      
    } else {
      if(cpeParameters.WPAAuthenticationMode.value == "EAPAuthentication") {
        security = "EAPAuthentication";
      } else {
        security = cpeParameters.WPAEncryptionModes.value;
      }
    }
  }

  log.info("--------------------- security = " + cpeParameters.WPAEncryptionModes.value);
  var parameter = {}; 
  parameter.writable = cpeParameters.BeaconType.writable;
  parameter.stale = cpeParameters.BeaconType.stale;
  parameter.value = security;
  parameter.disabled = false;
  parameter.dataType = {
    type: "ENUM",
    choice:[
      { systemName: "Disabled", friendlyName : "Disabled" },
      { systemName: "WEP-Open", friendlyName : "WEP-Open" },
      { systemName: "WEP-Shared", friendlyName : "WEP-Shared" },
      { systemName: "TKIPEncryption", friendlyName : "WPA-PSK(TKIP)" },
      { systemName: "AESEncryption", friendlyName : "WPA2-PSK(AES)" },
      { systemName: "TKIPandAESEncryption", friendlyName : "Mixed WPA/WPA2" },
      { systemName: "EAPAuthentication", friendlyName : "Enterprise (802.1x)" }
    ]
  };

  return parameter;
}

function update(cpeParameters) {

  log.info("CPE script parameters:");
  for(var name in scriptParameters) {
    log.info(" " + name + "=" + scriptParameters[name]);
  }

  for(name in scriptParameters) {
    var value = scriptParameters[name];
    switch (name){
    case "SSID": 
          cpeParameters.SSID.value = value;
          cpeParameters.SSID.updated = true;
          break;
        
    case "AutoChannel": 
          cpeParameters.AutoChannel.value = value;
          cpeParameters.AutoChannel.updated = true;
          break;
        
    case "Channel": 
          if(value &lt; 0 || value &gt; 11)
             throw "Channel number invalid. Must be 1 - 11";
          cpeParameters.Channel.value = value;
          cpeParameters.Channel.updated = true;
          break;
    case "Enabled":
          cpeParameters.Enabled.value = value === "true" ? 1 : 0;
          cpeParameters.Enabled.updated = true;
          break;
    case "AutoChannelRefreshPeriod": 
          cpeParameters.AutoChannelRefreshPeriod.value = value;
          cpeParameters.AutoChannelRefreshPeriod.updated = true;
          break;
    case "BroadcastSSID":
          cpeParameters.BroadcastSSID.value = value === "true" ? 1 : 0;
          cpeParameters.BroadcastSSID.updated = true;
          break;
    case "Standard":
          cpeParameters.Standard.value = value;
          cpeParameters.Standard.updated = true;
          break;
    case "SecurityMode":         
          if (value == "Disabled") {
            cpeParameters.BasicAuthenticationMode.value = "None";
            cpeParameters.BasicAuthenticationMode.updated = true;
            cpeParameters.BasicEncryptionModes.value = "None";
            cpeParameters.BasicEncryptionModes.updated = true;
            cpeParameters.BeaconType.value = "Basic";
            cpeParameters.BeaconType.updated = true;
          } else if(value == "WEP-Shared" || value == "WEP-Open") {
            if(typeof scriptParameters.CurrentPasswordIndex != 'undefined') {
              var PasswordIndex = parseInt(scriptParameters.CurrentPasswordIndex,10);
              if(PasswordIndex &lt; 1 &amp;&amp; PasswordIndex &gt; 4)
                throw "Key index must be between 1 and 4";
              cpeParameters.CurrentPasswordIndex.value = scriptParameters.CurrentPasswordIndex;
              cpeParameters.CurrentPasswordIndex.updated = true;
            } else {
              throw "Key index must be between 1 and 4";
            }

            if (typeof scriptParameters.Password1 != 'undefined' &amp;&amp; scriptParameters.Password1 != null) {
              if(scriptParameters.Password1.length !== 0 &amp;&amp; scriptParameters.Password1.length != 13 &amp;&amp; scriptParameters.Password1.length != 5)
                throw "Password1 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password1.value = scriptParameters.Password1;
              cpeParameters.Password1.updated = true;
            }
            if (typeof scriptParameters.Password2 != 'undefined' &amp;&amp; scriptParameters.Password2 != null) {
              if(scriptParameters.Password2.length !== 0 &amp;&amp; scriptParameters.Password2.length != 13 &amp;&amp; scriptParameters.Password2.length != 5)
                throw "Password2 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password2.value = scriptParameters.Password2;
              cpeParameters.Password2.updated = true;
            }
            if (typeof scriptParameters.Password3 != 'undefined' &amp;&amp; scriptParameters.Password3 != null) {
              if(scriptParameters.Password3.length !== 0 &amp;&amp; scriptParameters.Password3.length != 13 &amp;&amp; scriptParameters.Password3.length != 5)
                throw "Password3 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password3.value = scriptParameters.Password3;
              cpeParameters.Password3.updated = true;
            }
            if (typeof scriptParameters.Password4 != 'undefined' &amp;&amp; scriptParameters.Password4 != null) {
              if(scriptParameters.Password4.length !== 0 &amp;&amp; scriptParameters.Password4.length != 13 &amp;&amp; scriptParameters.Password4.length != 5)
                throw "Password4 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password4.value = scriptParameters.Password4;
              cpeParameters.Password4.updated = true;
            }

            if(value == "WEP-Shared") {
              cpeParameters.BasicAuthenticationMode.value = "SharedAuthentication";
              cpeParameters.BasicAuthenticationMode.updated = true;
            } else {
              cpeParameters.BasicAuthenticationMode.value = "None";
              cpeParameters.BasicAuthenticationMode.updated = true;
            }
            cpeParameters.BasicEncryptionModes.value = "WEPEncryption";
            cpeParameters.BasicEncryptionModes.updated = true;
            cpeParameters.BeaconType.value = "Basic";
            cpeParameters.BeaconType.updated = true;
          } else if(value == "EAPAuthentication") {
            cpeParameters.BeaconType.value = "WPA";
            cpeParameters.BeaconType.updated = true;
            cpeParameters.WPAAuthenticationMode.value = "EAPAuthentication";
            cpeParameters.WPAAuthenticationMode.updated = true;
            cpeParameters.WPAEncryptionModes.value = "TKIPandAESEncryption";
            cpeParameters.WPAEncryptionModes.updated = true;
            cpeParameters.BasicAuthenticationMode.value = "None";
            cpeParameters.BasicAuthenticationMode.updated = true;
            cpeParameters.BasicEncryptionModes.value = "None";
            cpeParameters.BasicEncryptionModes.updated = true;
          } else if(value == "TKIPEncryption" || value == "AESEncryption" || value == "TKIPandAESEncryption") {            
            cpeParameters.BeaconType.value = "WPA";
            cpeParameters.BeaconType.updated = true;
            cpeParameters.WPAAuthenticationMode.value = "PSKAuthentication";
            cpeParameters.WPAAuthenticationMode.updated = true;
            cpeParameters.WPAEncryptionModes.value = value;
            cpeParameters.WPAEncryptionModes.updated = true;
            cpeParameters.BasicAuthenticationMode.value = "None";
            cpeParameters.BasicAuthenticationMode.updated = true;
            cpeParameters.BasicEncryptionModes.value = "None";
            cpeParameters.BasicEncryptionModes.updated = true;

            if (typeof scriptParameters.Password != 'undefined' &amp;&amp; scriptParameters.Password !== null) {
              if(scriptParameters.Password.length &lt; 8)
                throw "Password length invalid. Must be 8-63 ASCII characters";
              cpeParameters.Password.value = scriptParameters.Password;
              cpeParameters.Password.updated = true;
            }
          }
          break;
       default : 
          break;
    }
  }
  return cpeParameters;
}

response;
</javaScriptCode>
        </scriptDefinition>
    </deviceServiceConfigurations>
    <deviceLogParameters name="Device Log 1" parameterName="InternetGatewayDevice.DeviceInfo.DeviceLog"/>
    <dataComposers name="Bytes Sent">
        <scriptDefinition name="TP-Link_IGD_LAB: Bytes Sent" purpose="Device service configuration" tags="null" scriptParameters="[]">
            <javaScriptCode>var acs = require("acs");
var composer = require("datacomposer");

var deviceId = scriptParameters.deviceId;
var cpeParameterNames = [
  { cpeParameterName: "InternetGatewayDevice.WANDevice.1.WANCommonInterfaceConfig.TotalBytesSent" }
];

var results = acs.getDeviceParametersFromRest({
  deviceId: deviceId,
  names: cpeParameterNames
});

var response = composer.newGraphResponse(results[0].value, Date.now());
response;
</javaScriptCode>
        </scriptDefinition>
    </dataComposers>
    <dataComposers name="Memoria Livre">
        <scriptDefinition name="TP-Link_IGD_CABO:Memoria Livre" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
            <javaScriptCode>var acs = require("acs");
var composer = require("datacomposer");

var freeMemory  = acs.searchParameters("InternetGatewayDevice.DeviceInfo.MemoryStatus.Free",null,scriptParameters.deviceId);
var totalMemory = acs.searchParameters("InternetGatewayDevice.DeviceInfo.MemoryStatus.Total",null,scriptParameters.deviceId);

//Percentage
var memoryAvailable = Math.round((freeMemory[0].value * 100)/totalMemory[0].value);

var response = composer.newNumericResponse(memoryAvailable,Date.now());
response;
</javaScriptCode>
        </scriptDefinition>
    </dataComposers>
    <dataComposers name="Bytes Received">
        <scriptDefinition name="TP-Link_IGD_LAB: Bytes Received" purpose="Device service configuration" tags="null" scriptParameters="[]">
            <javaScriptCode>var acs = require("acs");
var composer = require("datacomposer");

var deviceId = scriptParameters.deviceId;
var cpeParameterNames = [
  { cpeParameterName: "InternetGatewayDevice.WANDevice.1.WANCommonInterfaceConfig.TotalBytesReceived" }
];

var results = acs.getDeviceParametersFromRest({
  deviceId: deviceId,
  names: cpeParameterNames
});

var response = composer.newGraphResponse(results[0].value, Date.now());
response;
</javaScriptCode>
        </scriptDefinition>
    </dataComposers>
    <dashboardPanelScripts>
        <dashboardPanelScript name="##dashboard.device_info.name##" scriptType="DASHBOARD_SCRIPT">
            <scriptDefinition name="TP-Link_IGD_LAB:##dashboard.device_info.name##" purpose="Device service configuration" tags="null" scriptParameters="[]">
                <javaScriptCode>var acs = require('acs');

var deviceId = scriptParameters.deviceId;

var response = acs.getDeviceInfo(deviceId);
var ui_response = createDeviceInfoPanelUiResponse(response);

/**
 * Below is a sample response for device information rest call which can be used to populate device info panel.
 * For more information, please refer to Rest API documentation at {@link https://developer.incognito.com/acs/rest-api/acs-device#misc-device-information}
 * 
   {
    "protocol": "TR069",
    "tags": [],
    "oui": "FFFFFF",
    "productClass": "MockDevice",
    "serial": "1",
    "syncStatus": "SYNCHRONIZED",
    "connectivityStatus": "UNKNOWN",
    "firmwareVersion": "1.0.0.1",
    "manufacturer": "Incognito",
    "hardwareVersion": "1.0.0.0",
    "discovered": "2019-10-16T15:24:45",
    "lastModified": "2019-10-19T18:51:33",
    "lastModifiedBy": "Administrator",
    "dhcpOption82": null,
    "macAddr": "ff:ff:5f:e5:83:99",
    "ipAddr": "172.0.0.10, 192.168.0.16",
    "xmpp": false,
    "stun": true,
    "upTime": "5",
    "deviceModelSummary": {
        "name": "Incognito_MockDevice_FFFFFF",
        "id": "3535a4b9-6560-db31-60df-3712c7d1c303"
    },
    "clusterId": "default",
    "division": null,
    "nextExpectedInform": "2019-10-19T18:51:36",
    "imei": null,
    "iccid": null,
    "mqttInformInterval": null,
    "numMissedInform": null,
    "lastBoot": null,
    "subscriberId": null,
    "interfaces": [],
    "parameters": [
        {
            "name": "periodicInformInterval",
            "value": "30"
        },
        {
            "name": "connectionRequestUsername",
            "value": ""
        },
        {
            "name": "connectionRequestPassword",
            "value": ""
        },
        {
            "name": "cpeUsername",
            "value": "testUsr"
        },
        {
            "name": "cpePassword",
            "value": "testPwd"
        },
        {
            "name": "stunEnabled",
            "value": false
        },
        {
            "name": "stunServerAddress",
            "value": null
        },
        {
            "name": "stunServerPort",
            "value": "3478"
        },
        {
            "name": "stunUsername",
            "value": null
        },
        {
            "name": "stunPassword",
            "value": null
        },
        {
            "name": "xmppEnabled",
            "value": null
        },
        {
            "name": "xmppServerAddress",
            "value": null
        },
        {
            "name": "xmppServerPort",
            "value": null
        },
        {
            "name": "xmppUsername",
            "value": null
        },
        {
            "name": "xmppPassword",
            "value": null
        },
        {
            "name": "xmppDomain",
            "value": null
        },
        {
            "name": "xmppResource",
            "value": null
        },
        {
            "name": "xmppJabberId",
            "value": null
        },
        {
            "name": "discoveryMethod",
            "value": null
        },
        {
            "name": "ignoreError",
            "value": null
        },
        {
            "name": "cookiePath",
            "value": null
        },
        {
            "name": "batchSize",
            "value": null
        }
    ],
    "lastInformTime": "2019-10-19T18:51:06",
    "taskId": "2c26cd3e-e534-55ef-a759-d91bfe8a0471"
}
 */


function createDeviceInfoPanelUiResponse(deviceInfo) {

  var deviceInfoPanelData = {
    "tabs": [
      {
        "order": 0,
        "friendlyName": "Summary",
        "rows": [
          {
            "friendlyName": "Manufacturer",
            "value": deviceInfo.manufacturer
          },
          {
            "friendlyName": "IPs",
            "value": deviceInfo.ipAddr
          },
          {
            "friendlyName": "MACs",
            "value": deviceInfo.macAddr
          },
          {
            "friendlyName": "Firmware Version",
            "value": deviceInfo.firmwareVersion
          },
          {
            "friendlyName": "Hardware Version",
            "value": deviceInfo.hardwareVersion
          },
          {
            "friendlyName": "OUI",
            "value": deviceInfo.oui
          },
          {
            "friendlyName": "Product Class",
            "value": deviceInfo.productClass
          },
          {
            "friendlyName": "Serial",
            "value": deviceInfo.serial
          },
          {
            "friendlyName": "CWMP Cluster ID",
            "value": deviceInfo.clusterId
          }
        ]
      }
      /*,
      {
        "order": 1,
        "friendlyName": "XMPP",
        "rows": [
          {
            "friendlyName": "Enabled",
            "value": deviceInfo.xmpp
          },
          {
            "friendlyName": "Manufacturer",
            "value": deviceInfo.manufacturer
          },
          {
            "friendlyName": "Server Address",
            "value": getXmppServerAddress(deviceInfo.parameters)
          },
          {
            "friendlyName": "Server Port",
            "value": getXmppServerPort(deviceInfo.parameters)
          }
        ]
      }
      */
    ]
  };
  return deviceInfoPanelData;
}

/**
 * Helper method to extract a given parameter from device info parameters (deviceInfo.parameters)
 * 
 * @param parameterName
 * @param parameters
 * @returns
 */
function findDeviceInfoParameter(parameterName, parameters) {
  if (!Array.isArray(parameters)) {
    return undefined;
  }
  for (var i = 0; i &lt; parameters.length; i++) {
    if (parameters[i].name === parameterName) {
      return parameters[i].value;
    }
  }
  return undefined;
}


/**
 * Extract stunEnabled flag from device info parameters structure
 * 
 * @param parameters
 * @returns
 */
function getStunEnabled(parameters) {
  return findDeviceInfoParameter('stunEnabled', parameters) || false;
}


/**
 * Extract Server address from device info parameters
 * 
 * @param parameters
 * @returns
 */
function getXmppServerAddress(parameters) {
  return findDeviceInfoParameter('xmppServerAddress', parameters) || '';
}

/**
 * Extract Server Port from device info parameters
 * 
 * @param parameters
 * @returns
 */
function getXmppServerPort(parameters) {
  return findDeviceInfoParameter('xmppServerPort', parameters) || '';
}



ui_response;
</javaScriptCode>
            </scriptDefinition>
        </dashboardPanelScript>
        <dashboardPanelScript name="##dashboard.tr069_config.name##" scriptType="DASHBOARD_SCRIPT">
            <scriptDefinition name="TP-Link_IGD_LAB:##dashboard.tr069_config.name##" purpose="Device service configuration" tags="null" scriptParameters="[]">
                <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var data = {
  label: "TR69 Config",
  parameters: [
    { label: "Connection Request Username", cpeParameterName:"InternetGatewayDevice.ManagementServer.ConnectionRequestUsername" },
    { label: "Connection Request Password", cpeParameterName:"InternetGatewayDevice.ManagementServer.ConnectionRequestPassword" },
    { label: "Connection Request URL", cpeParameterName:"InternetGatewayDevice.ManagementServer.ConnectionRequestURL", readOnly: true },
    { label: "Periodic Inform Interval", cpeParameterName:"InternetGatewayDevice.ManagementServer.PeriodicInformInterval" },
    { label: "CPE Username", cpeParameterName:"InternetGatewayDevice.ManagementServer.Username" },
    { label: "CPE Password", cpeParameterName:"InternetGatewayDevice.ManagementServer.Password" }
  ]
};

var response = dsc.createResponse({
    data: data,
    scriptParameters: scriptParameters
});

response;
</javaScriptCode>
            </scriptDefinition>
        </dashboardPanelScript>
        <dashboardPanelScript name="##dashboard.connected_devices_topology.name##" scriptType="DASHBOARD_SCRIPT">
            <scriptDefinition name="TP-Link_IGD_LAB:##dashboard.connected_devices_topology.name##" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
                <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var data = {
  label: "Connected Devices",
  name: "ConnectedDevices",
  writable: false,
  readCallback: readTableCallback,
  parameters: [
    // Host name or interface name
    { name: "Name", label: "Name/Alias", cpeParameterName: "Device.X_Incognito.ConnectedDevices.Host.{i}.Name" },
    // Hard-coded: "INTERFACE" | "HOST"
    { name: "Type", label: "Type", cpeParameterName: "Device.X_Incognito.ConnectedDevices.Host.{i}.Type" },
    { name: "MACAddress", label: "MAC", cpeParameterName: "Device.X_Incognito.ConnectedDevices.Host.{i}.MACAddress" },
    { name: "IPAddress", label: "IP", cpeParameterName: "Device.X_Incognito.ConnectedDevices.Host.{i}.IPAddress" },
    { name: "Active", label: "Active", cpeParameterName: "Device.X_Incognito.ConnectedDevices.Host.{i}.Active" },
    { name: "InterfaceType", label: "Interface Type", cpeParameterName: "Device.X_Incognito.ConnectedDevices.Host.{i}.InterfaceType" },
    { name: "SignalStrength", label: "Signal Strength", cpeParameterName: "Device.X_Incognito.ConnectedDevices.Host.{i}.X_TP_StaSignalStrength" },
    { name: "AcsDeviceLink", label: "AcsDeviceLink", cpeParameterName: "Device.X_Incognito.ConnectedDevices.Host.{i}.AcsDeviceLink" },
    { name: "AcsDeviceType", label: "AcsDeviceType", cpeParameterName: "Device.X_Incognito.ConnectedDevices.Host.{i}.AcsDeviceType" }/*,
    { name: "BytesReceived", label: "Bytes Received", cpeParameterName: "Device.X_Incognito.ConnectedDevices.Host.{i}.WifiBytesReceived" },
    { name: "BytesSent", label: "Bytes Sent", cpeParameterName: "Device.X_Incognito.ConnectedDevices.Host.{i}.WifiBytesSent" }*/
  ]
};


var response = dsc.createResponse({
  data: data,
  scriptParameters: scriptParameters,
  isConnectedDevices: true,
  refreshInterval: 60
});

/*
{
   "description":"",
   "dataType":{
      "type":"TABLE",
      "elements":[
         {
            "name":"Name",
            "friendlyName":"Name/Alias",
            "writable":false,
            "dataType":{
               "type":"STRING"
            }
         },
         {
            "name":"Type",
            "friendlyName":"Type",
            "writable":false,
            "dataType":{
               "type":"STRING"
            }
         },
         {
            "name":"Category",
            "friendlyName":"Category",
            "writable":false,
            "dataType":{
               "type":"STRING"
            }
         },
         {
            "name":"MACAddress",
            "friendlyName":"MAC",
            "writable":false,
            "dataType":{
               "type":"STRING"
            }
         },
         {
            "name":"IPAddress",
            "friendlyName":"IP",
            "writable":false,
            "dataType":{
               "type":"STRING"
            }
         },
         {
            "name":"Active",
            "friendlyName":"Active",
            "writable":false,
            "dataType":{
               "type":"STRING"
            }
         },
         {
            "name":"InterfaceType",
            "friendlyName":"Interface Type",
            "writable":false,
            "dataType":{
               "type":"STRING"
            }
         },
         {
            "name":"SignalStrength",
            "friendlyName":"Signal Strength",
            "writable":false,
            "dataType":{
               "type":"STRING"
            }
         },
         {
            "name":"BytesReceived",
            "friendlyName":"Bytes Received",
            "writable":false,
            "dataType":{
               "type":"STRING"
            }
         },
         {
            "name":"BytesSent",
            "friendlyName":"Bytes Sent",
            "writable":false,
            "dataType":{
               "type":"STRING"
            }
         }
      ]
   },
   "value":[
      {
         "id":"1",
         "MACAddress":"ff:ee:25:00:00:01",
         "Type":"INTERFACE",
         "Name":"Ethernet 1"
      },
      {
         "id":"2",
         "Type":"HOST",
         "IPAddress":"192.0.0.2",
         "MACAddress":"ff:ff:ff:00:00:01",
         "Category":"apple-tv",
         "Name":"Device1",
         "InterfaceType":"Ethernet",
         "SignalStrength":null,
         "Active":"true"
      },
      {
         "id":"11",
         "BytesReceived":"13317137",
         "BytesSent":"753439697",
         "Type":"INTERFACE",
         "Name":"WiFi 2.4Ghz"
      },
      {
         "id":"12",
         "Type":"HOST",
         "IPAddress":"192.0.0.27",
         "MACAddress":"ff:ff:ff:00:00:1A",
         "Category":null,
         "Name":"Device26 (alias2)",
         "InterfaceType":"WIFI",
         "SignalStrength":null,
         "Active":"true"
      },
      {
         "id":"13",
         "Type":"HOST",
         "IPAddress":"192.0.0.39",
         "MACAddress":"ff:ff:ff:00:00:26",
         "Category":null,
         "Name":"Device38",
         "InterfaceType":"WIFI",
         "SignalStrength":null,
         "Active":"true"
      },
   ],
   "name":"ConnectedDevices",
   "friendlyName":"Connected Devices"
}
*/

function readTableCallback(table) {
  var tableSize = table.value.length;
  var connectedDevicesTables = [];
  var currentTableIdx = -1;
  for (var i = 0; i &lt; tableSize; i++) {
    var row = table.value[i];
    if (row.id === '*') {
      continue;
    }
    if (row.Type === 'INTERFACE') {
      connectedDevicesTables.push({
        name: row.Name,
        rows: []
      });
      currentTableIdx = connectedDevicesTables.length - 1;
    } else {
      if (connectedDevicesTables.length === 0) {
        throw 'The Connected Devices table is not categorized based on interfaces correctly';
      }
      delete row.id;
      connectedDevicesTables[currentTableIdx].rows.push(reformatRow(row));
    }
  }

  //table.columns = table.dataType.elements;
  table.dataType.type = 'MULTI-TABLE';
  table.order = 0;
  table.friendlyName = 'Table';

  table.dataType.columns = table.dataType.elements;
  delete table.dataType.elements;
  var numColumns = table.dataType.columns.length;

  for (var i = 0; i &lt; numColumns; i++) {
    setColumnHeaderStyle(table.dataType.columns[i]);
  }

  table.tables = connectedDevicesTables;
  delete table.value;

  return table;
}

/**
 * A function that restructures the service config output into a multi-table
 * output format that used 
 * 
 * @param row
 * @returns
 */
function reformatRow(row) {
  if (row === null || row === undefined || typeof row !== 'object') {
    return row;
  }
  delete row.Type;
  var newRow = {};
  for (var field in row) {
    newRow[field] = {
      value: row[field]
    };

    setCellStyle(field, newRow[field]);
  }
  newRow = postFormatRow(newRow);
  return newRow;
}

/**
 * A callback function to perform any custom post-processing
 * on a table row after the row construction
 * 
 * 
 * @param newRow
 * @returns
 */
function postFormatRow(newRow) {
  if (newRow.InterfaceType.value === 'Ethernet' &amp;&amp; newRow.SignalStrength !== undefined &amp;&amp; newRow.SignalStrength !== null) {
    newRow.SignalStrength.value = 'NA';
    newRow.SignalStrength.className = undefined;
  }
  return newRow;
}


/**
 * A function to customize the format and behavior 
 * 
 * @param columnHeader
 * @returns
 */
function setColumnHeaderStyle(columnHeader) {
  if (columnHeader) {
    columnHeader.align = 'center';
    if (columnHeader.name === 'Type' || columnHeader.name === 'AcsDeviceLink') {
      columnHeader.hidden = true;
    } else {
      columnHeader.hidden = false;
    }
  }
}

/**
 * This function serves as a callback to customize the style
 * of each cell in a table. The function can be used to do
 * the following:
 * 1. Reformat the value of the table cell
 * 2. Set the style of the specific cell. Supported style
 *    parameters include:
 *    a. align: 'right', 'center' 'left'
 *    b. className: 'status-failure-background',
 *       'status-warning-background',
 *       'status-success-background'.
 *       className is used to set the background color
 *       of the specified cell. More className parameters
 *       will be added in the future.
 * 
 * @param columnName
 * @param rowCell
 * @returns
 */
function setCellStyle(columnName, rowCell) {
  if (rowCell) {
    rowCell.align = 'center';
    if (columnName === 'SignalStrength') {
      var v = 0;
      if ((typeof rowCell.value) === 'number') {
        v = rowCell.value; 
      }
      if ((typeof rowCell.value) === 'string') {
        try {
          v = parseInt(rowCell.value,10); 
        } catch (error) {}
      }
      if (v &lt; -80) {
        rowCell.className = 'status-failure-background';
      } else if (v &lt; -67) {
        rowCell.className = 'status-warning-background';
      } else {
        rowCell.className = 'status-success-background';
      }
    }
  }
}

/**
 * TODO move this method to deviceserviceconfiguration module
 * 
 * @param response
 * @returns
 */
function reformatResponse(response) {
  response.tabs = response.parameters;
  delete response.parameters;
  if (response.tabs &amp;&amp; response.tabs.length &gt; 0) {
    var dataType = JSON.parse(JSON.stringify(response.tabs[0].dataType));
    dataType.type = 'GRAPH';
    var tables = JSON.parse(JSON.stringify(response.tabs[0].tables));

    response.tabs.push({
      order: 1,
      friendlyName: "Graph",
      dataType: dataType,
      tables: tables
    });
  }

}
reformatResponse(response);
response;</javaScriptCode>
            </scriptDefinition>
        </dashboardPanelScript>
    </dashboardPanelScripts>
    <scriptSupportedLanguages code="fr_ca"/>
    <scriptSupportedLanguages code="en"/>
    <scriptSupportedLanguages code="fr"/>
    <scriptSupportedLanguages code="es"/>
    <scriptSupportedLanguages code="zh"/>
    <supportedLanguages code="en">
        <keywords name="acs.diagnostic_state" description="Diagnostic State"/>
    </supportedLanguages>
    <supportedLanguages code="fr">
        <keywords name="acs.diagnostic_state" description="L'état de diagnostic"/>
    </supportedLanguages>
    <supportedLanguages code="fr-CA">
        <keywords name="acs.diagnostic_state" description="L'état de diagnostic"/>
    </supportedLanguages>
    <supportedLanguages code="es">
        <keywords name="acs.diagnostic_state" description="Estado de diagnóstico"/>
    </supportedLanguages>
    <supportedLanguages code="zh">
        <keywords name="acs.diagnostic_state" description="诊断状态"/>
    </supportedLanguages>
    <supportedLanguages code="tr">
        <keywords name="acs.diagnostic_state" description="Tanılama Durumu"/>
    </supportedLanguages>
    <dashboards name="default">
        <widgets name="Device Groups" type="DEVICE_GROUPS" description="Device Group Associations" stale="false">
            <configuration>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">10</value>
                </entry>
                <entry>
                    <key>readOnly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
                </entry>
                <entry>
                    <key>serviceId</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">null</value>
                </entry>
                <entry>
                    <key>selectable</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="Device Log" type="SERVICE_CONFIGURATION" description="Device Log" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">file</value>
                </entry>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">23</value>
                </entry>
                <entry>
                    <key>readOnly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">true</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">Device Log</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="Bytes Received" type="DATA_COMPOSER_GRAPH" stale="true">
            <configuration>
                <entry>
                    <key>yMin</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">0</value>
                </entry>
                <entry>
                    <key>unit</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">byte</value>
                </entry>
                <entry>
                    <key>graphType</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">linegraph</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>lowThreshold</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">0</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">Bytes Received</value>
                </entry>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">22</value>
                </entry>
                <entry>
                    <key>highThreshold</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">0</value>
                </entry>
                <entry>
                    <key>xMin</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">0</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="Operations History" type="HISTORICAL_OPERATIONS" description="History of device operations" stale="false">
            <configuration>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">2</value>
                </entry>
                <entry>
                    <key>readOnly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
                </entry>
                <entry>
                    <key>serviceId</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">null</value>
                </entry>
                <entry>
                    <key>selectable</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="Uptime" type="SINGLE_VALUE" stale="true">
            <configuration>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">12</value>
                </entry>
                <entry>
                    <key>unit</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">second</value>
                </entry>
                <entry>
                    <key>readOnly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">true</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>parameter</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">InternetGatewayDevice.DeviceInfo.UpTime</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="Failed operations" type="FAILED_OPERATIONS" description="Device operations that were executed and completed with error" stale="false">
            <configuration>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">1</value>
                </entry>
                <entry>
                    <key>readOnly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
                </entry>
                <entry>
                    <key>serviceId</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">null</value>
                </entry>
                <entry>
                    <key>selectable</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="Active operations" type="ACTIVE_OPERATIONS" description="Device operations waiting for device to contact ACS to be executed" stale="false">
            <configuration>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">0</value>
                </entry>
                <entry>
                    <key>readOnly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
                </entry>
                <entry>
                    <key>serviceId</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">null</value>
                </entry>
                <entry>
                    <key>selectable</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="DHCP" type="SERVICE_CONFIGURATION" description="Device DHCP" stale="true">
            <configuration>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">18</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">DHCP</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="WiFi 2" type="SERVICE_CONFIGURATION" description="Wireless Network" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">wifi-signal</value>
                </entry>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">16</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 2</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="WiFi 1" type="SERVICE_CONFIGURATION" description="Wireless Network" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">wifi-signal</value>
                </entry>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">17</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 1</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="Bytes Sent" type="DATA_COMPOSER_GRAPH" stale="true">
            <configuration>
                <entry>
                    <key>yMin</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">0</value>
                </entry>
                <entry>
                    <key>unit</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">byte</value>
                </entry>
                <entry>
                    <key>graphType</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">linegraph</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>lowThreshold</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">0</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">Bytes Sent</value>
                </entry>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">21</value>
                </entry>
                <entry>
                    <key>highThreshold</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">0</value>
                </entry>
                <entry>
                    <key>xMin</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">0</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="Bytes Received" type="SINGLE_VALUE" stale="true">
            <configuration>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">14</value>
                </entry>
                <entry>
                    <key>unit</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">byte</value>
                </entry>
                <entry>
                    <key>readOnly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">true</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>parameter</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">InternetGatewayDevice.WANDevice.1.WANCommonInterfaceConfig.TotalBytesReceived</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="TR-69 Config" type="SERVICE_CONFIGURATION" description="TR-69 Configuration" stale="true">
            <configuration>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">11</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">TR-69 Config</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="Diagnostics" type="DIAGNOSTICS" description="Device Diagnostics" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">stethoscope</value>
                </entry>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">19</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="WAN" type="SERVICE_CONFIGURATION" description="Wide Area Network" stale="true">
            <configuration>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">15</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WAN</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="Bytes Sent" type="SINGLE_VALUE" stale="true">
            <configuration>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">13</value>
                </entry>
                <entry>
                    <key>unit</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">byte</value>
                </entry>
                <entry>
                    <key>readOnly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">true</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>parameter</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">InternetGatewayDevice.WANDevice.1.WANCommonInterfaceConfig.TotalBytesSent</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="Connected Devices" type="CONNECTED_DEVICES" description="Connected Devices" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">three-desktops</value>
                </entry>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">20</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
            </configuration>
        </widgets>
        <allowAllGroups>TRUE</allowAllGroups>
        <config/>
    </dashboards>
    <dashboardPanels>
        <dashboardPanel name="Tráfego 2.4 Ghz" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"c5d72d94-f29a-6be9-1d3d-135cffd63fde","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/a240daa0-e1cc-11ec-9604-e1217449a260?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_min:'0',axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:0.5,formatter:bytes,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'Bytes%20sent',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Stats.X_TP_BytesSent,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max),(field:'61ca57f2-469d-11e7-af02-69e470af7417',id:'0ec7af60-a91f-11eb-9f07-b1343aa3e324',lag:'',type:serial_diff)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries),(axis_position:right,chart_type:line,color:'rgba(211,96,134,1)',fill:0.5,formatter:number,id:'975bd3b0-a91f-11eb-9f07-b1343aa3e324',label:'Bytes%20Received',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Stats.X_TP_BytesReceived,id:'975bd3b1-a91f-11eb-9f07-b1343aa3e324',type:max),(field:'975bd3b1-a91f-11eb-9f07-b1343aa3e324',id:a8a26f30-a91f-11eb-9f07-b1343aa3e324,lag:'',type:serial_diff)),point_size:1,separate_axis:0,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'TPLink%20Wlan%202.4%20GHz%20-%20Per%20Device',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.online.name##" panelType="PANEL_STATUS_ONLINE">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.sync_status.name##" panelType="PANEL_STATUS_SYNC">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Canal 5Ghz" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"c5d72d94-f29a-6be9-1d3d-135cffd63fde","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/3ed7cbd0-ddbd-11ec-9e26-017eb26ca6c8?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:'0.1',filter:(language:kuery,query:''),formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'',line_width:1,metrics:!((id:'61ca57f2-469d-11e7-af02-69e470af7417',type:count)),point_size:1,separate_axis:0,split_color_mode:kibana,split_filters:!((color:%2368BC00,filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%2036'),id:c0235550-902a-11ec-8823-65b10961c04e,label:'Canal%2036'),(color:'rgba(84,179,153,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%2040'),id:c94521e0-902a-11ec-8823-65b10961c04e,label:'Canal%2040'),(color:'rgba(211,96,134,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%2044'),id:d3408590-902a-11ec-8823-65b10961c04e,label:'Channel%2044'),(color:'rgba(145,112,184,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%2048'),id:d7d269c0-902a-11ec-8823-65b10961c04e,label:'Channel%2048'),(color:'rgba(202,142,174,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%2052'),id:dd5341d0-902a-11ec-8823-65b10961c04e,label:'Channel%2052'),(color:'rgba(214,191,87,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%2056'),id:e0a727c0-902a-11ec-8823-65b10961c04e,label:'Channel%2056'),(color:'rgba(185,168,136,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%2060'),id:e76b5540-902a-11ec-8823-65b10961c04e,label:'Channel%2060'),(color:'rgba(218,139,69,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%2064'),id:ea256c30-902a-11ec-8823-65b10961c04e,label:'Channel%2064'),(color:'rgba(170,101,86,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%20100'),id:eda32140-902a-11ec-8823-65b10961c04e,label:'Channel%20100'),(color:'rgba(231,102,76,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%20104'),id:f106bea0-902a-11ec-8823-65b10961c04e,label:'Channel%20104'),(color:'rgba(22,0,188,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%20108'),id:f3c1bff0-902a-11ec-8823-65b10961c04e,label:'Channel%20108'),(color:'rgba(231,240,129,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%20112'),id:cce01c50-90c1-11ec-8419-030540e36e5c,label:'Channel%20112'),(color:'rgba(115,232,113,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%20116'),id:d16667c0-90c1-11ec-8419-030540e36e5c,label:'Channel%20116'),(color:'rgba(130,80,107,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%20120'),id:d4d3c920-90c1-11ec-8419-030540e36e5c,label:'Channel%20120'),(color:'rgba(247,112,112,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%20124'),id:dd5c62f0-90c1-11ec-8419-030540e36e5c,label:'Channel%20124'),(color:'rgba(1,120,66,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%20128'),id:e29387d0-90c1-11ec-8419-030540e36e5c,label:'Channel%20128'),(color:'rgba(235,198,97,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%20132'),id:e7a6f810-90c1-11ec-8419-030540e36e5c,label:'Channel%20132'),(color:'rgba(205,98,139,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%20136'),id:ed97f710-90c1-11ec-8419-030540e36e5c,label:'Channel%20136'),(color:'rgba(50,62,122,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%20140'),id:f3d2a940-90c1-11ec-8419-030540e36e5c,label:'Channel%20140'),(color:'rgba(41,105,128,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%20144'),id:f5baa320-90c1-11ec-8419-030540e36e5c,label:'Channel%20144'),(color:'rgba(38,67,83,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%20149'),id:f9f3e000-90c1-11ec-8419-030540e36e5c,label:'Channel%20149'),(color:'rgba(96,125,61,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%20153'),id:'518470a0-b4e4-11ec-8956-e556ebb5a566',label:'Channel%20153'),(color:'rgba(246,151,182,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel:%20157'),id:'64c814a0-b4e4-11ec-8956-e556ebb5a566',label:'Channel%20157'),(color:'rgba(236,205,177,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel%20:%20161'),id:'7047f570-b4e4-11ec-8956-e556ebb5a566',label:'Channel%20161')),split_mode:filters,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Channel%205Ghz%20-TPLink%20-%20Per%20Device',type:metrics))\n"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Tráfego 5Ghz" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"c5d72d94-f29a-6be9-1d3d-135cffd63fde","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/d2672060-e1ca-11ec-9604-e1217449a260?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_min:'0',axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:0.5,formatter:bytes,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'Bytes%20sent',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Stats.X_TP_BytesSent,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max),(field:'61ca57f2-469d-11e7-af02-69e470af7417',id:'0ec7af60-a91f-11eb-9f07-b1343aa3e324',lag:'',type:serial_diff)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries),(axis_position:right,chart_type:line,color:'rgba(211,96,134,1)',fill:0.5,formatter:number,id:'975bd3b0-a91f-11eb-9f07-b1343aa3e324',label:'Bytes%20Received',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Stats.X_TP_BytesReceived,id:'975bd3b1-a91f-11eb-9f07-b1343aa3e324',type:max),(field:'975bd3b1-a91f-11eb-9f07-b1343aa3e324',id:a8a26f30-a91f-11eb-9f07-b1343aa3e324,lag:'',type:serial_diff)),point_size:1,separate_axis:0,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'TPLink%20Wlan%205GHz%20-%20Per%20Device',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Utilização de Memória" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"3950ea5d-4cd6-ce22-ce7e-28da02674b04","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/c4d259e0-de07-11ec-b38c-935be712e04a?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-72h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:'rgba(84,165,179,1)',fill:'0.8',formatter:bytes,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'Memoria%20Livre',line_width:1,metrics:!((field:params.InternetGatewayDevice.DeviceInfo.MemoryStatus.Free,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries),(axis_position:right,chart_type:line,color:'rgba(214,191,87,1)',fill:0.5,formatter:number,id:'873dbbb0-de07-11ec-ba4e-9f9b182ff852',label:'Mem%C3%B3ria%20Total',line_width:1,metrics:!((field:params.InternetGatewayDevice.DeviceInfo.MemoryStatus.Total,id:'873dbbb1-de07-11ec-ba4e-9f9b182ff852',type:max)),point_size:1,separate_axis:0,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Memory%20free%20-%20Per%20Device%20-%20TPLink',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Trace Route" panelType="PANEL_DASHBOARD_TRACEROUTE">
            <configuration>{"diagnosticsConfig":[{"id":"TraceRoute Diagnostics","subType":"TRACEROUTE","diagnosticParameters":[{"name":"InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount","value":""},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.Host","value":"8.8.8.8"},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.Timeout","value":""},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries","value":""},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize","value":""},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.DSCP","value":""}]}],"tabName":"312aaf62-50f6-cb11-b488-72b85b0678bb","InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount":"","InternetGatewayDevice.TraceRouteDiagnostics.Host":"8.8.8.8","InternetGatewayDevice.TraceRouteDiagnostics.Timeout":"","InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries":"","InternetGatewayDevice.TraceRouteDiagnostics.Interface":"","InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize":"","InternetGatewayDevice.TraceRouteDiagnostics.DSCP":""}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.active_operations.name##" panelType="PANEL_STATUS_OPERATIONS_ACTIVE">
            <configuration>{"links":{"#panelStatusOperationsActive":{"url":"#devices/{deviceId}/active-operations"}},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"rules":{"type":"numeric","threshold":"NONE"},"unit":null}</configuration>
        </dashboardPanel>
        <dashboardPanel name="WiFi 5 Ghz" panelType="PANEL_DASHBOARD_SERVICE_CONFIG">
            <configuration>{"readOnly":false,"tabName":"c5d72d94-f29a-6be9-1d3d-135cffd63fde","dataSource":{"type":"SERVICE_CONFIGURATION_SCRIPT","sourceId":"WiFi 5 TP","sourceIdSet":[]},"diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_SERVICE_CONFIG","dataType":"SERVICE_CONFIGURATION_SCRIPT","dataSourceServiceConfig":"4f7f50f5-3b41-bd6b-7916-601e97d2b36b"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="WiFi 2.4 Ghz" panelType="PANEL_DASHBOARD_SERVICE_CONFIG">
            <configuration>{"readOnly":false,"tabName":"c5d72d94-f29a-6be9-1d3d-135cffd63fde","dataSource":{"type":"SERVICE_CONFIGURATION_SCRIPT","sourceId":"WiFi 2.4 TP","sourceIdSet":[]},"diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_SERVICE_CONFIG","dataType":"SERVICE_CONFIGURATION_SCRIPT","dataSourceServiceConfig":"1f60c2b7-a0c7-ea12-e99e-0d63cb51ad4f"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Alerts" panelType="PANEL_STATUS_ALERTS">
            <configuration>{"rules":{"threshold":"NONE","ok":{"className":"ok"},"warning":{"className":"warning"},"failure":{"className":"failure"}},"category":"NUMERIC","limits":{}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.up_time.name##" panelType="PANEL_STATUS_UPTIME">
            <configuration>{"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.DeviceInfo.UpTime","sourceIdSet":[]},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"duration":{"enable":true,"unit":"seconds"}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Memória %" panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"units":"%","rules":{"threshold":"INCREASING","ok":{"className":"ok","message":"OK"},"warning":{"className":"warning","message":"Atenção","value":50},"failure":{"className":"failure","message":"Crítico","value":70}},"dataSource":{"type":"DATA_COMPOSER_SCRIPT","sourceId":"Memoria Livre","sourceIdSet":[]},"category":"NUMERIC","limits":{}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.tr069_config.name##" panelType="PANEL_DASHBOARD_TR069_CONFIG">
            <configuration>{"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"##dashboard.tr069_config.name##","sourceIdSet":[]},"buttons":{"handlers":[{"text":"Save","handler":"saveServiceConfigParameters","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"POST"},"visible":true,"tab":null},{"text":"Cancel","handler":"cancel","endpoint":{"url":"/deviceoperations/cancellation","verb":"POST"},"visible":false,"tab":null},{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"readOnly":false}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.failed_operations.name##" panelType="PANEL_STATUS_OPERATIONS_FAILED">
            <configuration>{"links":{"#panelStatusOperationsFailed":{"url":"#devices/{deviceId}/failed-operations"}},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"rules":{"type":"numeric","threshold":"NONE"},"unit":null}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.admin_actions.name##" panelType="PANEL_DEVICE_OPERATIONS_ADMIN">
            <configuration>{"actionsConfig":[{"id":"ManageOperation","text":"Manage Operations","url":"#devices/{deviceId}/active-operations","order":1,"visible":true},{"id":"ObjectStructParameter","text":"Manage Object Structure &amp; Parameters","url":"#devices/{deviceId}/parameters","order":2,"visible":true},{"id":"ManageGroupings","text":"Manage Groupings","url":"#devices/{deviceId}/device-groups","order":3,"visible":true},{"id":"ViewDeviceInfo","text":"View Device Information","url":"#devices/{deviceId}/device","order":4,"visible":true},{"id":"DeviceWorkbench","text":"Device Workbench","url":"#devices/{deviceId}/workbench","order":5,"visible":true},{"id":"ComplianceTestSuite","text":"Run Compliance Test Suite","url":"#devices/{deviceId}/execute-device-compliance-suite","order":6,"visible":true},{"id":"PerformActions","text":"Perform Actions","url":"#devices/{deviceId}/devicemodel/{deviceModelId}/device_actions","order":7,"visible":true},{"id":"PerformDiagnostics","text":"Perform Diagnostics","url":"#devices/{deviceId}/devicemodel/{deviceModelId}/diagnostics","order":8,"visible":true}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Broadband Speed Test" panelType="PANEL_DASHBOARD_BROADBAND_SPEED">
            <configuration>{"diagnosticsConfig":[{"id":"Download Diagnostics","subType":"DOWNLOADSPEED","diagnosticParameters":[{"name":"InternetGatewayDevice.DownloadDiagnostics.DownloadURL","value":"http://35.215.210.14:8080/download.bin"},{"name":"InternetGatewayDevice.DownloadDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.DownloadDiagnostics.DSCP","value":""},{"name":"InternetGatewayDevice.DownloadDiagnostics.EthernetPriority","value":""}]},{"id":"Upload Diagnostics","subType":"UPLOADSPEED","diagnosticParameters":[{"name":"InternetGatewayDevice.UploadDiagnostics.EthernetPriority","value":""},{"name":"InternetGatewayDevice.UploadDiagnostics.UploadURL","value":"http://35.215.210.14:8080/upload.bin"},{"name":"InternetGatewayDevice.UploadDiagnostics.DSCP","value":""},{"name":"InternetGatewayDevice.UploadDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.UploadDiagnostics.TestFileLength","value":""}]}],"tabName":"d3eacad3-9ffd-96b8-22fb-311cec6d1e61","InternetGatewayDevice.DownloadDiagnostics.DownloadURL":"http://35.215.210.14:8080/download.bin","InternetGatewayDevice.DownloadDiagnostics.Interface":"","InternetGatewayDevice.DownloadDiagnostics.DSCP":"","InternetGatewayDevice.DownloadDiagnostics.EthernetPriority":"","InternetGatewayDevice.UploadDiagnostics.EthernetPriority":"","InternetGatewayDevice.UploadDiagnostics.UploadURL":"http://35.215.210.14:8080/upload.bin","InternetGatewayDevice.UploadDiagnostics.DSCP":"","InternetGatewayDevice.UploadDiagnostics.Interface":"","InternetGatewayDevice.UploadDiagnostics.TestFileLength":""}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.common_issues.name##" panelType="PANEL_DEVICE_OPERATIONS_ISSUES">
            <configuration>{"actionsConfig":[{"order":0,"include":true,"text":"Incognito Support","url":"https://support.incognito.com/"}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Canal 2.4Ghz" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"c5d72d94-f29a-6be9-1d3d-135cffd63fde","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/c44a9eb0-ba99-11ec-96e0-c516b8f93291?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:'0.1',filter:(language:kuery,query:''),formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'',line_width:1,metrics:!((id:'61ca57f2-469d-11e7-af02-69e470af7417',type:count)),point_size:1,separate_axis:0,split_color_mode:kibana,split_filters:!((color:%2368BC00,filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%201'),id:c0235550-902a-11ec-8823-65b10961c04e,label:'Canal%201'),(color:'rgba(84,179,153,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%202'),id:c94521e0-902a-11ec-8823-65b10961c04e,label:'Canal%202'),(color:'rgba(211,96,134,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%203'),id:d3408590-902a-11ec-8823-65b10961c04e,label:'Canal%203'),(color:'rgba(145,112,184,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%204'),id:d7d269c0-902a-11ec-8823-65b10961c04e,label:'Canal%204'),(color:'rgba(202,142,174,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%205'),id:dd5341d0-902a-11ec-8823-65b10961c04e,label:'Canal%205'),(color:'rgba(214,191,87,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%206'),id:e0a727c0-902a-11ec-8823-65b10961c04e,label:'Canal%206'),(color:'rgba(185,168,136,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%207'),id:e76b5540-902a-11ec-8823-65b10961c04e,label:'Canal%207'),(color:'rgba(218,139,69,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%208'),id:ea256c30-902a-11ec-8823-65b10961c04e,label:'Canal%208'),(color:'rgba(170,101,86,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%209'),id:eda32140-902a-11ec-8823-65b10961c04e,label:'Canal%209'),(color:'rgba(231,102,76,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%2010'),id:f106bea0-902a-11ec-8823-65b10961c04e,label:'Canal%2010'),(color:'rgba(22,0,188,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%2011'),id:f3c1bff0-902a-11ec-8823-65b10961c04e,label:'Canal%2011')),split_mode:filters,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Channel%202.4%20Geral%20-%20Per%20Device',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.device_actions.name##" panelType="PANEL_DEVICE_OPERATIONS_ACTIONS">
            <configuration>{"actionsConfig":[{"id":"ReloadDataModel","order":1,"visible":true},{"id":"Reload","order":2,"visible":true},{"id":"Reboot","order":0,"visible":true}],"moreButton":{"handlers":[{"text":"##dashboard.more_device_actions##","handler":"showMoreActions","visible":false}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Uptime" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"3950ea5d-4cd6-ce22-ce7e-28da02674b04","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/91cc5b80-ca22-11eb-898c-b150debb2799?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:0.5,filter:(language:kuery,query:''),formatter:'s,h,1',id:'61ca57f1-469d-11e7-af02-69e470af7417',label:Uptime,line_width:1,metrics:!((field:params.InternetGatewayDevice.DeviceInfo.UpTime,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries,value_template:'%7B%7Bvalue%7D%7D%20horas')),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Uptime%20-%20Per%20Device',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Connected Devices Topology" panelType="PANEL_DASHBOARD_CONNECTED_DEVICES">
            <configuration>{"readOnly":false,"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"##dashboard.connected_devices_topology.name##","sourceIdSet":[]},"tabName":"29e57b2f-a14f-3433-9a2a-79147bd68b9a","diagnosticsConfig":[{"diagnosticParameters":[]}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Utilização de CPU" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"3950ea5d-4cd6-ce22-ce7e-28da02674b04","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/52d88d00-e299-11ec-9604-e1217449a260?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:0.5,formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'CPU%20%25',line_width:1,metrics:!((field:params.InternetGatewayDevice.DeviceInfo.ProcessStatus.CPUUsage,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'TPLink%20CPU%20-%20Individual',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="CPU %" panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"units":"%","rules":{"threshold":"INCREASING","ok":{"className":"ok","message":"OK"},"warning":{"className":"warning","message":"Atenção ","value":50},"failure":{"className":"failure","message":"Crítico","value":70}},"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.DeviceInfo.ProcessStatus.CPUUsage"},"category":"NUMERIC","limits":{}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.last_seen.name##" panelType="PANEL_STATUS_LASTSEEN">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"duration":{"enable":false,"unit":null}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Channel 5Ghz Errors " panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"c5d72d94-f29a-6be9-1d3d-135cffd63fde","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/fa49a8b0-7661-11ed-9e2d-6ffb69368d72?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:'rgba(96,146,192,1)',fill:'0',formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'Erros%20Enviados',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Stats.ErrorsSent,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries),(axis_position:right,chart_type:line,color:'rgba(211,96,134,1)',fill:'0',formatter:number,id:'99664230-9028-11ec-8823-65b10961c04e',label:'Erros%20Recebidos',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Stats.ErrorsReceived,id:'99664231-9028-11ec-8823-65b10961c04e',type:max)),point_size:1,separate_axis:0,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'TPLink%20-%20Pacotes%20Erros%205%20Ghz',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="IP Ping Test" panelType="PANEL_DASHBOARD_IPPING">
            <configuration>{"diagnosticsConfig":[{"id":"IP Ping Diagnostics","subType":"IPPING","diagnosticParameters":[{"name":"InternetGatewayDevice.IPPingDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.IPPingDiagnostics.Host","value":"8.8.8.8"},{"name":"InternetGatewayDevice.IPPingDiagnostics.DSCP","value":""},{"name":"InternetGatewayDevice.IPPingDiagnostics.DataBlockSize","value":"10000"},{"name":"InternetGatewayDevice.IPPingDiagnostics.Timeout","value":""},{"name":"InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions","value":""}]}],"tabName":"312aaf62-50f6-cb11-b488-72b85b0678bb","InternetGatewayDevice.IPPingDiagnostics.Interface":"","InternetGatewayDevice.IPPingDiagnostics.Host":"8.8.8.8","InternetGatewayDevice.IPPingDiagnostics.DSCP":"","InternetGatewayDevice.IPPingDiagnostics.DataBlockSize":"10000","InternetGatewayDevice.IPPingDiagnostics.Timeout":"","InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions":""}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Channel 2.4 Errors" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"c5d72d94-f29a-6be9-1d3d-135cffd63fde","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/5d5cf880-7662-11ed-9e2d-6ffb69368d72?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:'rgba(96,146,192,1)',fill:'0',formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'Erros%20Enviados',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Stats.ErrorsSent,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries),(axis_position:right,chart_type:line,color:'rgba(211,96,134,1)',fill:'0',formatter:number,id:'99664230-9028-11ec-8823-65b10961c04e',label:'Erros%20Recebidos',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Stats.ErrorsReceived,id:'99664231-9028-11ec-8823-65b10961c04e',type:max)),point_size:1,separate_axis:0,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'TPLink%20-%20Pacotes%20Erros%202.4%20Ghz',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.session_info.name##" panelType="PANEL_DASHBOARD_SESSION_INFO">
            <configuration>{"buttons":{"handlers":[{"text":"Initiate Session","handler":"initiateSession","endpoint":{"url":"/devices/{deviceId}/connectionrequest?async=true","verb":"POST"},"visible":true,"tab":null}]},"websockets":{"ws":"/devices/{deviceId}?X-Atmosphere-tracking-id=0&amp;X-Cache-Date=0&amp;Content-Type=application/json&amp;X-atmo-protocol=true","handlers":[{"type":"TR69_INFORM_EVENT"},{"type":"TR69_SESSION_EVENT"},{"type":"TR69_CONNECTION_REQUEST_EVENT"}]},"readOnly":false}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.device_info.name##" panelType="PANEL_DASHBOARD_DEVICE_INFO">
            <configuration>{"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"##dashboard.device_info.name##","sourceIdSet":[]},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"panelType":"PANEL_STATUS_ONLINE"}}]},"buttons":{"handlers":[{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"readOnly":true}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.broadband_speed_hist.name##" panelType="PANEL_DASHBOARD_BROADBAND_HISTORICAL">
            <configuration>{"buttons":{"handlers":[{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"tableConfig":{"searchName":"PANEL_DASHBOARD_BROADBAND_HISTORICAL","title":"Historic Broadband Speed Test Results","searchParams":{"tableName":"DIAGNOSTIC_RESULT_SUMMARY","url":"/devices/{deviceId}/diagnostics/speedtest","q":"PINGTESTDATE is null","pageSize":20,"orderBy":"LASTMODIFIED","ascending":false},"columns":[{"name":"time","field":"lastModified","label":"Time","align":"left","dataType":"DATETIME","fieldFormat":"hh:mma, dd MMM yyyy"},{"name":"dload","field":"downloadSpeed","label":"Download Speed (Mbps)","align":"center","dataType":"MBYTES","fieldFormat":"%.1f"},{"name":"uload","field":"uploadSpeed","label":"Upload Speed (Mbps)","align":"center","dataType":"MBYTES","fieldFormat":"%.1f"}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Connected Devices" panelType="PANEL_STATUS_CONNECTED">
            <configuration>{"rules":{"threshold":"INCREASING","ok":{"className":"ok","message":"OK"},"warning":{"className":"warning","message":"Atenção","value":50},"failure":{"className":"failure","message":"Crítico","value":70}},"category":"NUMERIC","limits":{}}</configuration>
        </dashboardPanel>
    </dashboardPanels>
    <dashboardLayout>{"version":"1.2","children":[{"type":"COLUMN_LEFT","order":0,"hasPanelChildren":false,"children":[{"name":"##dashboard.layout.region.device_ident##","type":"REGION_DEVICE_IDENTIFIER","order":0,"hasPanelChildren":false,"children":[{"name":"PANEL_COMMON_DEVICE_IDENTIFIER","type":"PANEL_COMMON_DEVICE_IDENTIFIER","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.customer_ident##","type":"REGION_CUSTOMER_IDENTIIFIER","order":1,"hasPanelChildren":true,"children":[{"name":"PANEL_COMMON_CUSTOMER_IDENTIFIER","type":"PANEL_COMMON_CUSTOMER_IDENTIFIER","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.images##","type":"REGION_DEVICE_IMAGES","order":2,"hasPanelChildren":true,"children":[{"name":"PANEL_COMMON_DEVICE_IMAGES","type":"PANEL_COMMON_DEVICE_IMAGES","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.operations##","type":"REGION_DEVICE_OPERATIONS","order":3,"hasPanelChildren":true,"children":[{"name":"##dashboard.device_actions.name##","type":"PANEL_DEVICE_OPERATIONS_ACTIONS","order":0,"hasPanelChildren":false},{"name":"##dashboard.common_issues.name##","type":"PANEL_DEVICE_OPERATIONS_ISSUES","order":1,"hasPanelChildren":false},{"name":"##dashboard.admin_actions.name##","type":"PANEL_DEVICE_OPERATIONS_ADMIN","order":2,"hasPanelChildren":false}]}]},{"type":"COLUMN_RIGHT","order":1,"hasPanelChildren":false,"children":[{"name":"##dashboard.layout.region.status##","type":"REGION_STATUS","order":0,"hasPanelChildren":true,"children":[{"name":"##dashboard.online.name##","type":"PANEL_STATUS_ONLINE","order":0,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.last_seen.name##","type":"PANEL_STATUS_LASTSEEN","order":1,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.sync_status.name##","type":"PANEL_STATUS_SYNC","order":2,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.active_operations.name##","type":"PANEL_STATUS_OPERATIONS_ACTIVE","order":3,"hasPanelChildren":false,"visible":true},{"name":"Connected Devices","type":"PANEL_STATUS_CONNECTED","order":4,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.up_time.name##","type":"PANEL_STATUS_UPTIME","order":5,"hasPanelChildren":false,"visible":true},{"name":"CPU %","type":"PANEL_STATUS_CUSTOM","order":6,"hasPanelChildren":false,"visible":true,"category":"NUMERIC"},{"name":"Memória %","type":"PANEL_STATUS_CUSTOM","order":7,"hasPanelChildren":false,"visible":true,"category":"NUMERIC"},{"name":"##dashboard.failed_operations.name##","type":"PANEL_STATUS_OPERATIONS_FAILED","order":8,"hasPanelChildren":false,"visible":true},{"name":"Alerts","type":"PANEL_STATUS_ALERTS","order":9,"hasPanelChildren":false,"visible":true}]},{"name":"##dashboard.layout.region.csr_call_log##","type":"REGION_CSR_CALL_INFO","order":1,"hasPanelChildren":true,"children":[{"name":"##dashboard.csr_call_info.name##","type":"PANEL_COMMON_CSR_CALL_INFO","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.dashboards##","type":"REGION_DASHBOARDS","order":2,"hasPanelChildren":false,"children":[{"name":"##dashboard.tab.overview##","type":"TAB_DASHBOARD","order":0,"hasPanelChildren":true,"visible":true,"children":[{"name":"##dashboard.device_info.name##","type":"PANEL_DASHBOARD_DEVICE_INFO","order":0,"hasPanelChildren":false,"visible":true,"size":{"h":1,"v":1}},{"name":"##dashboard.session_info.name##","type":"PANEL_DASHBOARD_SESSION_INFO","order":1,"hasPanelChildren":false,"visible":true,"size":{"h":1,"v":1}},{"name":"Broadband Speed Test","type":"PANEL_DASHBOARD_BROADBAND_SPEED","order":2,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"##dashboard.broadband_speed_hist.name##","type":"PANEL_DASHBOARD_BROADBAND_HISTORICAL","order":3,"hasPanelChildren":false,"visible":true,"size":{"h":1,"v":1}}]},{"name":"##dashboard.tab.topology##","type":"TAB_DASHBOARD","order":1,"hasPanelChildren":true,"visible":false,"children":[{"name":"Connected Devices Topology","type":"PANEL_DASHBOARD_CONNECTED_DEVICES","order":0,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":2}}]},{"name":"##dashboard.tab.diagnostics##","type":"TAB_DASHBOARD","order":2,"hasPanelChildren":true,"visible":false,"children":[{"name":"##dashboard.tr069_config.name##","type":"PANEL_DASHBOARD_TR069_CONFIG","order":0,"hasPanelChildren":false,"size":{"h":1,"v":1}},{"name":"IP Ping Test","type":"PANEL_DASHBOARD_IPPING","order":1,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"Trace Route","type":"PANEL_DASHBOARD_TRACEROUTE","order":2,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}}]},{"name":"WiFi","type":"TAB_DASHBOARD","order":3,"hasPanelChildren":true,"visible":true,"children":[{"name":"WiFi 2.4 Ghz","type":"PANEL_DASHBOARD_SERVICE_CONFIG","order":0,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"WiFi 5 Ghz","type":"PANEL_DASHBOARD_SERVICE_CONFIG","order":1,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"Canal 2.4Ghz","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":2,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Tráfego 2.4 Ghz","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":3,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Channel 2.4 Errors","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":4,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Canal 5Ghz","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":5,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Tráfego 5Ghz","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":6,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Channel 5Ghz Errors ","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":7,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":2,"v":1}}]},{"name":"Graficos","type":"TAB_DASHBOARD","order":4,"hasPanelChildren":true,"visible":true,"children":[{"name":"Uptime","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":0,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Utilização de CPU","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":1,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Utilização de Memória","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":2,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}}]}]}]}]}</dashboardLayout>
    <imageReferences friendlyName="Captura de Tela 2022-06-07 às 13.39.43.png" extension="png" description="" index="1" fileName="Captura de Tela 2022-06-07 às 13.39.43.png.png"/>
    <imageReferences friendlyName="Captura de Tela 2022-06-07 às 13.39.16.png" extension="png" description="" index="0" fileName="Captura de Tela 2022-06-07 às 13.39.16.png.png"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DNSServers" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DNSServers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeKey" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeKey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeKey" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_Local.Language" elementDefinition="InternetGatewayDevice.X_TP_Local.Language" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_Local.Language" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.ErrorsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.ErrorsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.ErrorsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.MaximumActiveConnections" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.MaximumActiveConnections" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.MemoryStatus.Total" elementDefinition="InternetGatewayDevice.DeviceInfo.MemoryStatus.Total" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.MemoryStatus.Total" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.EOMTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.EOMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.EOMTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.DuplexMode" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.DuplexMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.BOMTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.BOMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.BOMTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.EnablePerConnectionResults" elementDefinition="InternetGatewayDevice.UploadDiagnostics.EnablePerConnectionResults" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.EnablePerConnectionResults" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_FullconeNATEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_FullconeNATEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_FullconeNATEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_TotalBytesSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_TotalBytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_TotalBytesSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MACAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MACAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.Alias" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.Alias" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.Alias" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestMeasurementInterval" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestMeasurementInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestMeasurementInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.OpenVPNSSLFiles.SSLServer.Cert" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.OpenVPNSSLFiles.SSLServer.Cert" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.OpenVPNSSLFiles.SSLServer.Cert" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBroadcastPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBroadcastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBroadcastPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Client.{i}.ConnAct" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.Client.{i}.ConnAct" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Client.{i}.ConnAct" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_UserCfg.AdminName" elementDefinition="InternetGatewayDevice.X_TP_UserCfg.AdminName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_UserCfg.AdminName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.UploadDiagnostics.DSCP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.DSCP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.ProtocolVersion" elementDefinition="InternetGatewayDevice.UploadDiagnostics.ProtocolVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.ProtocolVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.MaxMarkingEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.MaxMarkingEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MaxAddress_BK" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MaxAddress_BK" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MaxAddress_BK" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.OpenVPNSSLFiles.CertAuth.Cert" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.OpenVPNSSLFiles.CertAuth.Cert" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.OpenVPNSSLFiles.CertAuth.Cert" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_ConnectionId" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_ConnectionId" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_ConnectionId" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.DeviceLog" elementDefinition="InternetGatewayDevice.DeviceInfo.DeviceLog" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MACAddressControlEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MACAddressControlEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.Enable" elementDefinition="InternetGatewayDevice.UDPEchoConfig.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoConfig.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_TotalPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_TotalPacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_TotalPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNUsername" elementDefinition="InternetGatewayDevice.ManagementServer.STUNUsername" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.STUNUsername" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.EnablePerConnectionResults" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.EnablePerConnectionResults" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.EnablePerConnectionResults" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.Interface" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpRefererCheckEnabled" elementDefinition="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpRefererCheckEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpRefererCheckEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DNSServers" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DNSServers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.AdditionalHardwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.AdditionalHardwareVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.RegistrarNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.RegistrarNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.RegistrarNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UploadTransports" elementDefinition="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UploadTransports" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UploadTransports" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.Username" elementDefinition="InternetGatewayDevice.ManagementServer.Username" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPLeaseTime_BK" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPLeaseTime_BK" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPLeaseTime_BK" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.PeriodicInformInterval" elementDefinition="InternetGatewayDevice.ManagementServer.PeriodicInformInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDeviceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDeviceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_FullconeNATEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_FullconeNATEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_FullconeNATEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_VID" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_VID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_VID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSentUnderFullLoading" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSentUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSentUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.TimeFirstPacketReceived" elementDefinition="InternetGatewayDevice.UDPEchoConfig.TimeFirstPacketReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoConfig.TimeFirstPacketReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.RouteProtocolRx" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.RouteProtocolRx" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.DownloadTransports" elementDefinition="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.DownloadTransports" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.DownloadTransports" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPConditionalPoolNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPConditionalPoolNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPConditionalPoolNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestMeasurementOffset" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestMeasurementOffset" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestMeasurementOffset" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetUnicastPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetUnicastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetUnicastPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Client.{i}.PppdPid" elementDefinition="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Client.{i}.PppdPid" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Client.{i}.PppdPid" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DefaultGateway" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DefaultGateway" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.AdditionalSoftwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.AdditionalSoftwareVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKeyIndex" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKeyIndex" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.SSIDAdvertisementEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.SSIDAdvertisementEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.SSIDAdvertisementEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.SubnetMask" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.SubnetMask" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_PreSSID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_PreSSID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_PreSSID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.PortMappingNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.PortMappingNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.SuccessCount" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.SuccessCount" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_TP_WANPPTPConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_TP_WANPPTPConnectionNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_TP_WANPPTPConnectionNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_UserCfg.UserName" elementDefinition="InternetGatewayDevice.X_TP_UserCfg.UserName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_UserCfg.UserName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.DataBlockSize" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.DataBlockSize" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.Protocol" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.Protocol" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.Protocol" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeBSSID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeBSSID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeBSSID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_RTSThreshold" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_RTSThreshold" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_RTSThreshold" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_ClonedMACAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_ClonedMACAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_ClonedMACAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddress" elementDefinition="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.DiscardPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.DiscardPacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.DiscardPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.HardwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.HardwareVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.DiscardPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.DiscardPacketsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.DiscardPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Enable" elementDefinition="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.MaximumResponseTime" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.MaximumResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Username" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Username" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Username" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_PdOnlyEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_PdOnlyEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_PdOnlyEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_ClonedMACAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_ClonedMACAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_ClonedMACAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.FastestHost" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.FastestHost" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.FastestHost" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_UseStaticIP" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_UseStaticIP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_UseStaticIP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.LocalTimeZoneName" elementDefinition="InternetGatewayDevice.Time.LocalTimeZoneName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.IncrementalResultNumberOfEntries" elementDefinition="InternetGatewayDevice.UploadDiagnostics.IncrementalResultNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.IncrementalResultNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterStatus" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ExternalIPAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ExternalIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.HWQoS_iptv.DownTotalBW" elementDefinition="InternetGatewayDevice.HWQoS_iptv.DownTotalBW" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.HWQoS_iptv.DownTotalBW" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Uptime" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Uptime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.SoftwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.SoftwareVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Access" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.Access" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Access" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.KeepAliveInterval" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.KeepAliveInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.KeepAliveInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceived" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DomainName" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DomainName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.DaylightSavingsUsed" elementDefinition="InternetGatewayDevice.Time.DaylightSavingsUsed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.X_TP_CurSentSpeed" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.X_TP_CurSentSpeed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.X_TP_CurSentSpeed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_Hostname" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_Hostname" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_Hostname" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.RemoteIpEnd" elementDefinition="InternetGatewayDevice.X_TP_VPN.PPTPVPN.RemoteIpEnd" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.RemoteIpEnd" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PossibleChannels" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PossibleChannels" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.IsolateClients" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.IsolateClients" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.IsolateClients" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnectionNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.SourceIPAddress" elementDefinition="InternetGatewayDevice.UDPEchoConfig.SourceIPAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoConfig.SourceIPAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnicastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnicastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnicastPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.Weight" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.Weight" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.Weight" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WlBrName.{i}.BridgeName" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WlBrName.{i}.BridgeName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WlBrName.{i}.BridgeName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetUnknownProtoPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetUnknownProtoPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetUnknownProtoPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_LANAccessEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_LANAccessEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_LANAccessEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.HWQoS_iptv.IptvBW" elementDefinition="InternetGatewayDevice.HWQoS_iptv.IptvBW" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.HWQoS_iptv.IptvBW" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBytesSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBytesSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_BcastAddr" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_BcastAddr" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_BcastAddr" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.PeriodOfFullLoading" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.PeriodOfFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.PeriodOfFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.Timeout" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.Timeout" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_TP_Local.IspName" elementDefinition="InternetGatewayDevice.X_TP_Local.IspName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_Local.IspName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.WPAAuthenticationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.WPAAuthenticationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.WPAAuthenticationMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.URL" elementDefinition="InternetGatewayDevice.ManagementServer.URL" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.IEEE11iAuthenticationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.IEEE11iAuthenticationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.IEEE11iAuthenticationMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Port" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.Port" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Port" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.SuccessCount" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.SuccessCount" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.SuccessCount" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Name" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.TransportType" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.TransportType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPAuthenticationProtocol" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPAuthenticationProtocol" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPowerSupported" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPowerSupported" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPowerSupported" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_GroupKeyUpdateInterval" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_GroupKeyUpdateInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_GroupKeyUpdateInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNServerPort" elementDefinition="InternetGatewayDevice.ManagementServer.STUNServerPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.STUNServerPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_TP_CurSentSpeed" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_TP_CurSentSpeed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_TP_CurSentSpeed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.PacketsReceived" elementDefinition="InternetGatewayDevice.UDPEchoConfig.PacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoConfig.PacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeName" elementDefinition="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_Configuration_Modified" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_Configuration_Modified" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_Configuration_Modified" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPEncryptionLevel" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPEncryptionLevel" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.UploadURL" elementDefinition="InternetGatewayDevice.UploadDiagnostics.UploadURL" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.UploadURL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBroadcastPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBroadcastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBroadcastPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.PossibleConnectionTypes" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.PossibleConnectionTypes" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicDataTransmitRates" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicDataTransmitRates" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ProcessStatus.ProcessNumberOfEntries" elementDefinition="InternetGatewayDevice.DeviceInfo.ProcessStatus.ProcessNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.ProcessStatus.ProcessNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_TP_CurRecvSpeed" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_TP_CurRecvSpeed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_TP_CurRecvSpeed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TestFileLength" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TestFileLength" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TestFileLength" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_DTIMFrequency" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_DTIMFrequency" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_DTIMFrequency" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.OpenVPNSSLFiles.SSLClient.PrivateKey" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.OpenVPNSSLFiles.SSLClient.PrivateKey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.OpenVPNSSLFiles.SSLClient.PrivateKey" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDeviceNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDeviceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.X_TP_CurRecvSpeed" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.X_TP_CurRecvSpeed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.X_TP_CurRecvSpeed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ConnectionStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ConnectionStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_NeighbourScanEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_NeighbourScanEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_NeighbourScanEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKey.{i}.WEPKey" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKey.{i}.WEPKey" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MACAddressControlEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MACAddressControlEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.ServerConnectAlgorithm" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.ServerConnectAlgorithm" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.ServerConnectAlgorithm" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceivedUnderFullLoading" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceivedUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceivedUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Status" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Status" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_AppCfg.LocalHost" elementDefinition="InternetGatewayDevice.X_TP_AppCfg.LocalHost" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_AppCfg.LocalHost" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_BcastAddr" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_BcastAddr" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_BcastAddr" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPLeaseTime" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPLeaseTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.IPAddressUsed" elementDefinition="InternetGatewayDevice.UploadDiagnostics.IPAddressUsed" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.IPAddressUsed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DNSEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DNSEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Status" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnectionRequestUsername" elementDefinition="InternetGatewayDevice.ManagementServer.ConnectionRequestUsername" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_Band" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_Band" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_Band" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.AverageResponseTime" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.AverageResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_PdOnlyEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_PdOnlyEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_PdOnlyEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_RxRate" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_RxRate" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_RxRate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterKey" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterKey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.FilterNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.FilterNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceived" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestDuration" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestDuration" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestDuration" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_TP_RemoteDns" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_TP_RemoteDns" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_TP_RemoteDns" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BeaconType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BeaconType" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.UDPPort" elementDefinition="InternetGatewayDevice.UDPEchoConfig.UDPPort" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoConfig.UDPPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.UploadDiagnostics.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.DiagnosticsState" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.ServerRetryMaxInterval" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.ServerRetryMaxInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.ServerRetryMaxInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_UserCfg.UserPwd" elementDefinition="InternetGatewayDevice.X_TP_UserCfg.UserPwd" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_UserCfg.UserPwd" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.Port" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.Port" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.Port" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_IGMPForceVersion" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_IGMPForceVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_IGMPForceVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_TP_EWAN.Enable" elementDefinition="InternetGatewayDevice.X_TP_EWAN.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_EWAN.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_SecondConnectionDNSServers" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_SecondConnectionDNSServers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_SecondConnectionDNSServers" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_TP_RemoteGw" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_TP_RemoteGw" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_TP_RemoteGw" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Status" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Status" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.MaximumResponseTime" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.MaximumResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.MaximumResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterBridgeReference" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterBridgeReference" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.IndividualPacketResultNumberOfEntries" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.IndividualPacketResultNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.IndividualPacketResultNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.Enable" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DSCP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.DSCP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.__apLastStatus" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.__apLastStatus" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.__apLastStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_MACAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_MACAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_MACAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_IGMPForceVersion" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_IGMPForceVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_IGMPForceVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.X_TP_ConnType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.X_TP_ConnType" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.X_TP_ConnType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.EnableCWMP" elementDefinition="InternetGatewayDevice.ManagementServer.EnableCWMP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.EnableCWMP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.MulticastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.MulticastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.MulticastPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_EWAN.MACAddress" elementDefinition="InternetGatewayDevice.X_TP_EWAN.MACAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_EWAN.MACAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeKey" elementDefinition="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeKey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Password" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_RadiusServerPort" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_RadiusServerPort" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_RadiusServerPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicAuthenticationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicAuthenticationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceivedUnderFullLoading" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceivedUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceivedUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_Local.Country" elementDefinition="InternetGatewayDevice.X_TP_Local.Country" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_Local.Country" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.IEEE11iEncryptionModes" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.IEEE11iEncryptionModes" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.IEEE11iEncryptionModes" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.RadiusServerPassword" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.RadiusServerPassword" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.RadiusServerPassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadTransports" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DownloadTransports" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.DownloadTransports" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.DSCP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_CurSentSpeed" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_CurSentSpeed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_CurSentSpeed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.UseTLS" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.UseTLS" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.UseTLS" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.LANAccessEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.LANAccessEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.LANAccessEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_ConnectionId" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_ConnectionId" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_ConnectionId" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeEncryptMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeEncryptMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeEncryptMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.RegistrarEstablished" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.RegistrarEstablished" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.RegistrarEstablished" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadDiagnosticsMaxIncrementalResult" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DownloadDiagnosticsMaxIncrementalResult" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.DownloadDiagnosticsMaxIncrementalResult" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MACAddressControlRule" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MACAddressControlRule" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MACAddressControlRule" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANUSBInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANUSBInterfaceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Proto" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.Proto" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Proto" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.AssociatedDeviceMACAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.AssociatedDeviceMACAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.FailureCount" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.FailureCount" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.FailureCount" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnectionNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_TotalPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_TotalPacketsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_TotalPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.ProductClass" elementDefinition="InternetGatewayDevice.DeviceInfo.ProductClass" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.MACAddressOverride" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.MACAddressOverride" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPoEServiceName" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPoEServiceName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.ProtocolVersion" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.ProtocolVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.ProtocolVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Name" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Name" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Name" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.DefaultConnectionService" elementDefinition="InternetGatewayDevice.Layer3Forwarding.DefaultConnectionService" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_TP_WANL2TPConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_TP_WANL2TPConnectionNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_TP_WANL2TPConnectionNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.JabberID" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.JabberID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.JabberID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.MACAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.MACAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBytesSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBytesSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_PreSharedKey" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_PreSharedKey" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_PreSharedKey" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.Interface" elementDefinition="InternetGatewayDevice.UDPEchoConfig.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoConfig.Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.LocalTimeZone" elementDefinition="InternetGatewayDevice.Time.LocalTimeZone" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.MaxMTUSize" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.MaxMTUSize" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ParameterKey" elementDefinition="InternetGatewayDevice.ManagementServer.ParameterKey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.Timeout" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.Timeout" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.Timeout" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_FirewallEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_FirewallEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_FirewallEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BSSID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BSSID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetErrorsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetErrorsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetErrorsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MaxAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MaxAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TotalBytesSent" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TotalBytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TotalBytesSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBytesReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBytesReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_ShortGIEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_ShortGIEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_ShortGIEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.UploadTransports" elementDefinition="InternetGatewayDevice.UploadDiagnostics.UploadTransports" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.UploadTransports" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Username" elementDefinition="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Username" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Username" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.PhysicalLinkStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.PhysicalLinkStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.LastChangeDate" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.LastChangeDate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.LastChangeDate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.UpTime" elementDefinition="InternetGatewayDevice.DeviceInfo.UpTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceivedUnderFullLoading" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceivedUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceivedUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_SecondConnectionDefaultGateway" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_SecondConnectionDefaultGateway" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_SecondConnectionDefaultGateway" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ExternalIPAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ExternalIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.ServerRetryIntervalMultiplier" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.ServerRetryIntervalMultiplier" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.ServerRetryIntervalMultiplier" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetMulticastPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetMulticastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetMulticastPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.Host" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.Host" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.TraceRouteDiagnostics.Host" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterInterface" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterInterface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadDiagnosticMaxConnections" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DownloadDiagnosticMaxConnections" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.DownloadDiagnosticMaxConnections" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.RadiusServerIP" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.RadiusServerIP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.RadiusServerIP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.EchoPlusEnabled" elementDefinition="InternetGatewayDevice.UDPEchoConfig.EchoPlusEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoConfig.EchoPlusEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MACTableSize" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MACTableSize" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MACTableSize" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.MarkingNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.MarkingNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.UpgradesManaged" elementDefinition="InternetGatewayDevice.ManagementServer.UpgradesManaged" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.MulticastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.MulticastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.MulticastPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Client.{i}.WanIp" elementDefinition="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Client.{i}.WanIp" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Client.{i}.WanIp" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.SpecVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.SpecVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Standard" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Standard" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.MACAddressOverride" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.MACAddressOverride" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.MaxBridgeEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.MaxBridgeEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Client.{i}.WanPort" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.Client.{i}.WanPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Client.{i}.WanPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.Host" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.Host" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Name" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_StaHostName" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_StaHostName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_StaHostName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.SubnetAddress" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.SubnetAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.SubnetAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANWLANConfigurationNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANWLANConfigurationNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_StaSignalStrength" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_StaSignalStrength" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_StaSignalStrength" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WlBrName.{i}.IfName" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WlBrName.{i}.IfName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WlBrName.{i}.IfName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.ROMTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.ROMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.ROMTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.EnabledForInternet" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.EnabledForInternet" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeName" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.Interface" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.Interface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PossibleConnectionTypes" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PossibleConnectionTypes" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNPassword" elementDefinition="InternetGatewayDevice.ManagementServer.STUNPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.STUNPassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_TotalBytesReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_TotalBytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_TotalBytesReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ConnectionTrigger" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ConnectionTrigger" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ConnectionTrigger" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ConnectionTrigger" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TestBytesSentUnderFullLoading" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TestBytesSentUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TestBytesSentUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.ModemFirmwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.ModemFirmwareVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.BytesResponded" elementDefinition="InternetGatewayDevice.UDPEchoConfig.BytesResponded" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoConfig.BytesResponded" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.Timeout" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.Timeout" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.Timeout" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Enable" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.PacketsResponded" elementDefinition="InternetGatewayDevice.UDPEchoConfig.PacketsResponded" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoConfig.PacketsResponded" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_TP_DHCPAuto" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_TP_DHCPAuto" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_TP_DHCPAuto" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.SubnetMask" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.SubnetMask" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.SubnetMask" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.DataBlockSize" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.DataBlockSize" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.DataBlockSize" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetMulticastPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetMulticastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetMulticastPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnicastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnicastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnicastPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_UserCfg.AdminPwd" elementDefinition="InternetGatewayDevice.X_TP_UserCfg.AdminPwd" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_UserCfg.AdminPwd" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.BroadcastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.BroadcastPacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.BroadcastPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.ServerNumberOfEntries" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.ServerNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.ServerNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_CurRecvSpeed" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_CurRecvSpeed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_CurRecvSpeed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.BroadcastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.BroadcastPacketsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.BroadcastPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_Unicast" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_Unicast" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_Unicast" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadURL" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DownloadURL" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.DownloadURL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.X_TP_IfName" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.X_TP_IfName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.X_TP_IfName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Alias" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Alias" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Alias" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBroadcastPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBroadcastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBroadcastPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterfaceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Stats.TransmittedErrorMessages" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Stats.TransmittedErrorMessages" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Stats.TransmittedErrorMessages" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPower" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPower" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPower" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetMulticastPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetMulticastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetMulticastPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ConnectionType" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ConnectionType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.WANAccessProvider" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.WANAccessProvider" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNEnable" elementDefinition="InternetGatewayDevice.ManagementServer.STUNEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.STUNEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetErrorsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetErrorsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetErrorsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.CurrentMRUSize" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.CurrentMRUSize" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPRouters" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPRouters" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_TP_AppCfg.RemoteHost" elementDefinition="InternetGatewayDevice.X_TP_AppCfg.RemoteHost" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_AppCfg.RemoteHost" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.InterTransmissionTime" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.InterTransmissionTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.InterTransmissionTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Stats.ReceivedMessages" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Stats.ReceivedMessages" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Stats.ReceivedMessages" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.UDPEchoDiagnosticsMaxResults" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.UDPEchoDiagnosticsMaxResults" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.UDPEchoDiagnosticsMaxResults" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.PeriodOfFullLoading" elementDefinition="InternetGatewayDevice.UploadDiagnostics.PeriodOfFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.PeriodOfFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.X_TP_NegoSpeed" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.X_TP_NegoSpeed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.X_TP_NegoSpeed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterEnable" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.EnabledOptions" elementDefinition="InternetGatewayDevice.DeviceInfo.EnabledOptions" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.X_TP_ConnIntf" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.X_TP_ConnIntf" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.X_TP_ConnIntf" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IP_BK" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IP_BK" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IP_BK" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestDuration" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestDuration" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestDuration" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Enable" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1UpstreamMaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1UpstreamMaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.KickURL" elementDefinition="InternetGatewayDevice.ManagementServer.KickURL" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.MaximumResponseTime" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.MaximumResponseTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.MaximumResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAEncryptionModes" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAEncryptionModes" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPStaticAddressNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPStaticAddressNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPStaticAddressNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAAuthenticationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAAuthenticationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.MinimumResponseTime" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.MinimumResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.MinimumResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.EthernetLinkStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.EthernetLinkStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnectionRequestURL" elementDefinition="InternetGatewayDevice.ManagementServer.ConnectionRequestURL" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_TxRate" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_TxRate" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_TxRate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.Active" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.Active" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpLocalPort" elementDefinition="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpLocalPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpLocalPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.Interface" elementDefinition="InternetGatewayDevice.UploadDiagnostics.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_IfName" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_IfName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_IfName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenResponseTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TCPOpenResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.CurrentLocalTime" elementDefinition="InternetGatewayDevice.Time.CurrentLocalTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.NumberOfActiveConnections" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.NumberOfActiveConnections" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ConnectionStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ConnectionStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_TP_DefaultIp" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_TP_DefaultIp" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_TP_DefaultIp" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.NATEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.NATEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.NumberOfRepetitions" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.NumberOfRepetitions" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.NumberOfRepetitions" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestMeasurementInterval" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestMeasurementInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestMeasurementInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetUnicastPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetUnicastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetUnicastPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetUnicastPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetUnicastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetUnicastPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.X_TP_PeerPassword" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.X_TP_PeerPassword" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.X_TP_PeerPassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_AntiInterference" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_AntiInterference" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_AntiInterference" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_StaStandard" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_StaStandard" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_StaStandard" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.AddressingType" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.AddressingType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.LastConnectionError" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.LastConnectionError" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.Status" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.Status" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.Status" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.ManageableDeviceNumberOfEntries" elementDefinition="InternetGatewayDevice.ManagementServer.ManageableDeviceNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.ManageableDeviceNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.SetupLock" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.SetupLock" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.SetupLock" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpRemoteEnabled" elementDefinition="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpRemoteEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpRemoteEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.MACAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.MACAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.DSCP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.TraceRouteDiagnostics.DSCP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.RemoteIpStart" elementDefinition="InternetGatewayDevice.X_TP_VPN.PPTPVPN.RemoteIpStart" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.RemoteIpStart" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeStatus" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.HostList" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.HostList" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.HostList" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.DeviceName" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.DeviceName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.DeviceName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.OpenVPNSSLFiles.SSLClient.Cert" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.OpenVPNSSLFiles.SSLClient.Cert" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.OpenVPNSSLFiles.SSLClient.Cert" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBytesReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBytesReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MaxBitRate" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.Host" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.Host" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.Host" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.MACAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.MACAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_IfName" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_IfName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_IfName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.Priority" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.Priority" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.Priority" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Client.{i}.ConnAct" elementDefinition="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Client.{i}.ConnAct" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Client.{i}.ConnAct" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.BeaconType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.BeaconType" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.BeaconType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.HostName" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.HostName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_SecondConnectionSubnetMask" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_SecondConnectionSubnetMask" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_SecondConnectionSubnetMask" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.Interface" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.NTPServer5" elementDefinition="InternetGatewayDevice.Time.NTPServer5" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_TP_AgileACS_Sig" elementDefinition="InternetGatewayDevice.DeviceInfo.X_TP_AgileACS_Sig" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_TP_AgileACS_Sig" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.ManufacturerOUI" elementDefinition="InternetGatewayDevice.DeviceInfo.ManufacturerOUI" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.IPAddressUsed" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.IPAddressUsed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.IPAddressUsed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.NTPServer1" elementDefinition="InternetGatewayDevice.Time.NTPServer1" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.ROMTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.ROMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.ROMTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.NTPServer2" elementDefinition="InternetGatewayDevice.Time.NTPServer2" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.WANAccessType" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.WANAccessType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.NTPServer3" elementDefinition="InternetGatewayDevice.Time.NTPServer3" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.NTPServer4" elementDefinition="InternetGatewayDevice.Time.NTPServer4" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_RadiusServerIP" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_RadiusServerIP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_RadiusServerIP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MaxStaNum" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MaxStaNum" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MaxStaNum" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.Name" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.Name" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.Name" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSent" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetDiscardPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetDiscardPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetDiscardPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_EWAN.IfName" elementDefinition="InternetGatewayDevice.X_TP_EWAN.IfName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_EWAN.IfName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBroadcastPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBroadcastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBroadcastPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.MaxMRUSize" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.MaxMRUSize" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_FragmentThreshold" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_FragmentThreshold" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_FragmentThreshold" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iAuthenticationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iAuthenticationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.AverageResponseTime" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.AverageResponseTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.AverageResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.IncrementalResultNumberOfEntries" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.IncrementalResultNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.IncrementalResultNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpLocalEnabled" elementDefinition="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpLocalEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpLocalEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_Local.IspIndex" elementDefinition="InternetGatewayDevice.X_TP_Local.IspIndex" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_Local.IspIndex" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.NATDetected" elementDefinition="InternetGatewayDevice.ManagementServer.NATDetected" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.NATDetected" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnectionRequestPassword" elementDefinition="InternetGatewayDevice.ManagementServer.ConnectionRequestPassword" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.ForwardNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer3Forwarding.ForwardNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.AvailableInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.AvailableInterfaceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.IPAddressUsed" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.IPAddressUsed" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.IPAddressUsed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeSSID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeSSID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeSSID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Stats.TransmittedMessages" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Stats.TransmittedMessages" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Stats.TransmittedMessages" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_RipngEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_RipngEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_RipngEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.WEPKey.{i}.WEPKey" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.WEPKey.{i}.WEPKey" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.WEPKey.{i}.WEPKey" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.BytesReceived" elementDefinition="InternetGatewayDevice.UDPEchoConfig.BytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoConfig.BytesReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TotalBytesSentUnderFullLoading" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TotalBytesSentUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TotalBytesSentUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.MaxStaNum" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.MaxStaNum" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.MaxStaNum" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenRequestTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TCPOpenRequestTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenRequestTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_TP_DhcpRelayServer" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_TP_DhcpRelayServer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_TP_DhcpRelayServer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpsRemotePort" elementDefinition="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpsRemotePort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpsRemotePort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.Version" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.Version" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.Version" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TestBytesSent" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TestBytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TestBytesSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpsLocalPort" elementDefinition="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpsLocalPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpsLocalPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Client.{i}.TunIp" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.Client.{i}.TunIp" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Client.{i}.TunIp" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_IPTVMulticastEnable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_IPTVMulticastEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_IPTVMulticastEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.PerConnectionResultNumberOfEntries" elementDefinition="InternetGatewayDevice.UploadDiagnostics.PerConnectionResultNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.PerConnectionResultNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeStatus" elementDefinition="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.InterfaceType" elementDefinition="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.InterfaceType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.NumberOfConnections" elementDefinition="InternetGatewayDevice.UploadDiagnostics.NumberOfConnections" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.NumberOfConnections" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.MaxFilterEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.MaxFilterEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.AssociatedDeviceIPAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.AssociatedDeviceIPAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceSubnetMask" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceSubnetMask" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.DaylightSavingsStart" elementDefinition="InternetGatewayDevice.Time.DaylightSavingsStart" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.ErrorsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.ErrorsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.ErrorsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpsRemoteEnabled" elementDefinition="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpsRemoteEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpsRemoteEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestMeasurementOffset" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestMeasurementOffset" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestMeasurementOffset" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Domain" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Domain" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Domain" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.RemoteIPAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.RemoteIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSIDAdvertisementEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSIDAdvertisementEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSIDAdvertisementEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.BOMTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.BOMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.BOMTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DNSEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DNSEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.LeaseTimeRemaining" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.LeaseTimeRemaining" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPoEACName" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPoEACName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DNSOverrideAllowed" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DNSOverrideAllowed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.PeriodicInformEnable" elementDefinition="InternetGatewayDevice.ManagementServer.PeriodicInformEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.MinimumResponseTime" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.MinimumResponseTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.MinimumResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.DSCP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.DSCP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_BytesSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_BytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_BytesSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerEnable_BK" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerEnable_BK" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerEnable_BK" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.DiagnosticsState" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.HWQoS_iptv.Enable" elementDefinition="InternetGatewayDevice.HWQoS_iptv.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.HWQoS_iptv.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.EOMTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.EOMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.EOMTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetDiscardPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetDiscardPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetDiscardPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceSummary" elementDefinition="InternetGatewayDevice.DeviceSummary" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.NumberOfRepetitions" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.NumberOfRepetitions" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.NumberOfRepetitions" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.RSIPAvailable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.RSIPAvailable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_StaBandWidth" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_StaBandWidth" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_StaBandWidth" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.OpenVPNSSLFiles.SSLServer.PrivateKey" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.OpenVPNSSLFiles.SSLServer.PrivateKey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.OpenVPNSSLFiles.SSLServer.PrivateKey" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.SubnetMask_BK" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.SubnetMask_BK" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.SubnetMask_BK" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DNSServers_BK" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DNSServers_BK" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DNSServers_BK" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DNSServers" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DNSServers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_L2IfName" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_L2IfName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_L2IfName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_Bandwidth" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_Bandwidth" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_Bandwidth" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.X_TP_DaylightSavingsEndWeekCount" elementDefinition="InternetGatewayDevice.Time.X_TP_DaylightSavingsEndWeekCount" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Time.X_TP_DaylightSavingsEndWeekCount" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.AvailableInterfaceKey" elementDefinition="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.AvailableInterfaceKey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.EthernetPriority" elementDefinition="InternetGatewayDevice.UploadDiagnostics.EthernetPriority" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.EthernetPriority" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Uptime" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Uptime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.EnableIndividualPacketResults" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.EnableIndividualPacketResults" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.EnableIndividualPacketResults" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetMulticastPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetMulticastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetMulticastPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.DaylightSavingsEnd" elementDefinition="InternetGatewayDevice.Time.DaylightSavingsEnd" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.BasicAuthenticationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.BasicAuthenticationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.BasicAuthenticationMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeAuthMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeAuthMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeAuthMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.LocalIp" elementDefinition="InternetGatewayDevice.X_TP_VPN.PPTPVPN.LocalIp" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.LocalIp" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.SSID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.SSID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.SSID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.GroupKeyUpdateInterval" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.GroupKeyUpdateInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.GroupKeyUpdateInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNMaximumKeepAlivePeriod" elementDefinition="InternetGatewayDevice.ManagementServer.STUNMaximumKeepAlivePeriod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.STUNMaximumKeepAlivePeriod" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.IdleDisconnectTime" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.IdleDisconnectTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ProcessStatus.CPUUsage" elementDefinition="InternetGatewayDevice.DeviceInfo.ProcessStatus.CPUUsage" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.ProcessStatus.CPUUsage" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.SerialNumber" elementDefinition="InternetGatewayDevice.DeviceInfo.SerialNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_PacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_PacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_PacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.RouteProtocolRx" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.RouteProtocolRx" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNServerAddress" elementDefinition="InternetGatewayDevice.ManagementServer.STUNServerAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.STUNServerAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.UploadDiagnosticsMaxIncrementalResult" elementDefinition="InternetGatewayDevice.UploadDiagnostics.UploadDiagnosticsMaxIncrementalResult" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.UploadDiagnosticsMaxIncrementalResult" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.Interface" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MinAddress_BK" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MinAddress_BK" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MinAddress_BK" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.Timeout" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.Timeout" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.TraceRouteDiagnostics.Timeout" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DNSOverrideAllowed" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DNSOverrideAllowed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.ProtocolVersion" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.ProtocolVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.ProtocolVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeEnable" elementDefinition="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.Password" elementDefinition="InternetGatewayDevice.ManagementServer.Password" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPLCPEchoRetry" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPLCPEchoRetry" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.PerConnectionResultNumberOfEntries" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.PerConnectionResultNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.PerConnectionResultNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_BytesReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_BytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_BytesReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.LastConnectionError" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.LastConnectionError" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.Manufacturer" elementDefinition="InternetGatewayDevice.DeviceInfo.Manufacturer" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.DevicePassword" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.DevicePassword" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.DevicePassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPLCPEcho" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPLCPEcho" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.PeriodicInformTime" elementDefinition="InternetGatewayDevice.ManagementServer.PeriodicInformTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.MinimumResponseTime" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.MinimumResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceAddressingType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceAddressingType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.X_TP_DaylightSavingsStartWeekCount" elementDefinition="InternetGatewayDevice.Time.X_TP_DaylightSavingsStartWeekCount" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Time.X_TP_DaylightSavingsStartWeekCount" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.X_AcsPeriodicInformInterval" elementDefinition="InternetGatewayDevice.ManagementServer.X_AcsPeriodicInformInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.X_AcsPeriodicInformInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.CaGenerating" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.CaGenerating" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.CaGenerating" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.WEPKeyIndex" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.WEPKeyIndex" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.WEPKeyIndex" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.NATEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.NATEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_StaConnectionSpeed" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_StaConnectionSpeed" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_TP_StaConnectionSpeed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicEncryptionModes" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicEncryptionModes" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Username" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Username" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1DownstreamMaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1DownstreamMaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Password" elementDefinition="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceived" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.FirstUseDate" elementDefinition="InternetGatewayDevice.DeviceInfo.FirstUseDate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.NumberOfConnections" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.NumberOfConnections" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.NumberOfConnections" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_TP_ProductID" elementDefinition="InternetGatewayDevice.DeviceInfo.X_TP_ProductID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_TP_ProductID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetErrorsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetErrorsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetErrorsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Channel" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Channel" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.Interface" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.TraceRouteDiagnostics.Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_IPTVMulticastVID" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_IPTVMulticastVID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_IPTVMulticastVID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.ProvisioningCode" elementDefinition="InternetGatewayDevice.DeviceInfo.ProvisioningCode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Password" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PortMappingNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PortMappingNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.AverageResponseTime" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.AverageResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.AverageResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Stats.ReceivedErrorMessages" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Stats.ReceivedErrorMessages" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Stats.ReceivedErrorMessages" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_IGMPProxyEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_IGMPProxyEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_IGMPProxyEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MACAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MACAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.EthernetPriority" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.EthernetPriority" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.EthernetPriority" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_IfName" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_IfName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_IfName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetDiscardPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetDiscardPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetDiscardPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TCPOpenRequestTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TCPOpenRequestTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TCPOpenRequestTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.IPAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.IPAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.VLANID" elementDefinition="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.VLANID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.MemoryStatus.Free" elementDefinition="InternetGatewayDevice.DeviceInfo.MemoryStatus.Free" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.MemoryStatus.Free" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iEncryptionModes" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iEncryptionModes" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_IGMPProxyEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_IGMPProxyEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_IGMPProxyEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.DiagnosticsState" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.DiagnosticsState" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.IPAddressUsed" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.IPAddressUsed" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.IPAddressUsed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.HostNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.HostNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.DuplexMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.DuplexMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ConnectionType" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ConnectionType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigurationState" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigurationState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigurationState" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.TLSEstablished" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.TLSEstablished" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.TLSEstablished" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.ServerAddress" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.ServerAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Server.{i}.ServerAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.SubnetMask" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.SubnetMask" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnknownProtoPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnknownProtoPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnknownProtoPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddressNotificationLimit" elementDefinition="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddressNotificationLimit" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddressNotificationLimit" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.Port" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.Port" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.Port" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.RadiusServerPort" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.RadiusServerPort" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.RadiusServerPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.TimeLastPacketReceived" elementDefinition="InternetGatewayDevice.UDPEchoConfig.TimeLastPacketReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoConfig.TimeLastPacketReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.ResponseTime" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.ResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.TraceRouteDiagnostics.ResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Client.{i}.WanIp" elementDefinition="InternetGatewayDevice.X_TP_VPN.OpenVPN.Client.{i}.WanIp" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.OpenVPN.Client.{i}.WanIp" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.ServerConnectAttempts" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.ServerConnectAttempts" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.ServerConnectAttempts" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNMinimumKeepAlivePeriod" elementDefinition="InternetGatewayDevice.ManagementServer.STUNMinimumKeepAlivePeriod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.STUNMinimumKeepAlivePeriod" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_IsolateClients" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_IsolateClients" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_IsolateClients" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.ModelName" elementDefinition="InternetGatewayDevice.DeviceInfo.ModelName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_QosMark" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_QosMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_QosMark" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceIPAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpRemotePort" elementDefinition="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpRemotePort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpRemotePort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPRelay" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPRelay" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetDiscardPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetDiscardPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetDiscardPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_PacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_PacketsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_TP_PacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MinAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MinAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.InterfaceReference" elementDefinition="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.InterfaceReference" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.Description" elementDefinition="InternetGatewayDevice.DeviceInfo.Description" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.DiagnosticsState" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.Resource" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.Resource" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.Resource" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.X_TP_State" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.X_TP_State" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.X_TP_State" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetErrorsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetErrorsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetErrorsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.EchoPlusSupported" elementDefinition="InternetGatewayDevice.UDPEchoConfig.EchoPlusSupported" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoConfig.EchoPlusSupported" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.RouteHopsNumberOfEntries" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.RouteHopsNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.TraceRouteDiagnostics.RouteHopsNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.BridgeNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.BridgeNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetUnknownProtoPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetUnknownProtoPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetUnknownProtoPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.IdleDisconnectTime" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.IdleDisconnectTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.AddressSource" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.AddressSource" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Status" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.BasicEncryptionModes" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.BasicEncryptionModes" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.BasicEncryptionModes" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpsLocalEnabled" elementDefinition="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpsLocalEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_AppCfg.HttpCfg.HttpsLocalEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.ProtocolVersion" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.ProtocolVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.ProtocolVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WMMEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WMMEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WMMEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.XMPP.Connection.{i}.ServerRetryInitialInterval" elementDefinition="InternetGatewayDevice.XMPP.Connection.{i}.ServerRetryInitialInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.Connection.{i}.ServerRetryInitialInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetUnicastPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetUnicastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetUnicastPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeRSSI" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeRSSI" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeRSSI" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.TraceRouteDiagnostics.DiagnosticsState" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.PreSharedKey" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.PreSharedKey" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.PreSharedKey" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DefaultGateway" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DefaultGateway" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DefaultGateway" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.UploadDiagnosticsMaxConnections" elementDefinition="InternetGatewayDevice.UploadDiagnostics.UploadDiagnosticsMaxConnections" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.UploadDiagnosticsMaxConnections" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_VLanEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_VLanEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_TP_VLanEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_FirewallEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_FirewallEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_TP_FirewallEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Client.{i}.PtpIp" elementDefinition="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Client.{i}.PtpIp" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_TP_VPN.PPTPVPN.Client.{i}.PtpIp" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeWepKeyIndex" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeWepKeyIndex" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeWepKeyIndex" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TCPOpenResponseTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TCPOpenResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TCPOpenResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_BeaconInterval" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_BeaconInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_BeaconInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeAddrMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeAddrMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_WDSBridge.BridgeAddrMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.WPAEncryptionModes" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.WPAEncryptionModes" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_MultiSSID.MultiSSIDEntry.{i}.WPAEncryptionModes" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_TransportType" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_TransportType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_TP_TransportType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.FailureCount" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.FailureCount" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_RadiusServerPassword" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_RadiusServerPassword" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_TP_RadiusServerPassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.DownloadDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="Download Diagnostics" subType="DOWNLOADSPEED">
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.DSCP" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadURL" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.EthernetPriority" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.Interface" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.ROMTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.EOMTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceived"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceived"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.BOMTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenRequestTime"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.IPPingDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="IP Ping Diagnostics" subType="IPPING">
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.DSCP" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.Host" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.Timeout" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.Interface" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.DataBlockSize" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.MinimumResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.AverageResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.SuccessCount"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.FailureCount"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.MaximumResponseTime"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.TraceRouteDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="TraceRoute Diagnostics" subType="TRACEROUTE">
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.Timeout" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.DSCP" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.Interface" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.Host" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.TraceRouteDiagnostics.RouteHopsNumberOfEntries"/>
        <returnParameterNames name="InternetGatewayDevice.TraceRouteDiagnostics.ResponseTime"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.UploadDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="Upload Diagnostics" subType="UPLOADSPEED">
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.Interface" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.TestFileLength" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.EthernetPriority" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.DSCP" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.UploadURL" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.EOMTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.TCPOpenRequestTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.TotalBytesSent"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.BOMTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.ROMTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.TCPOpenResponseTime"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelNetworkInterfaces isWAN="false" type="Ethernet" name="Ethernet 12" description="network interface definition">
        <properties name="Port Bytes sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.12.Stats.BytesSent" parameterType="BYTES_SENT"/>
        <properties name="MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.12.MACAddress" parameterType="MAC_ADDRESS"/>
        <properties name="Port Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.12.Status" parameterType="OTHER"/>
        <properties name="Port Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.12.Stats.BytesReceived" parameterType="BYTES_RECEIVED"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="Ethernet" name="Ethernet 2" description="network interface definition">
        <properties name="MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.MACAddress" parameterType="MAC_ADDRESS"/>
        <properties name="Port Bytes sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.Stats.BytesSent" parameterType="BYTES_SENT"/>
        <properties name="Port Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.Stats.BytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Port Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.Status" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 2" description="network interface definition">
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Status" parameterType="OTHER"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.SSID" parameterType="SSID"/>
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.BSSID" parameterType="OTHER"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Enable" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 1" description="network interface definition">
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.BSSID" parameterType="OTHER"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.SSID" parameterType="SSID"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Status" parameterType="OTHER"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Enable" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="Ethernet" name="Ethernet 1" description="network interface definition">
        <properties name="Port Bytes sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.Stats.BytesSent" parameterType="BYTES_SENT"/>
        <properties name="Port Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.Stats.BytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.MACAddress" parameterType="MAC_ADDRESS"/>
        <properties name="Port Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.Status" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="Ethernet" name="Ethernet 11" description="network interface definition">
        <properties name="Port Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.11.Status" parameterType="OTHER"/>
        <properties name="Port Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.11.Stats.BytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.11.MACAddress" parameterType="MAC_ADDRESS"/>
        <properties name="Port Bytes sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.11.Stats.BytesSent" parameterType="BYTES_SENT"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="Ethernet" name="Ethernet 10" description="network interface definition">
        <properties name="Port Bytes sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.10.Stats.BytesSent" parameterType="BYTES_SENT"/>
        <properties name="Port Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.10.Stats.BytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.10.MACAddress" parameterType="MAC_ADDRESS"/>
        <properties name="Port Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.10.Status" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
</DeviceModel>