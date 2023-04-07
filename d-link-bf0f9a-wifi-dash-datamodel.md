<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<DeviceModel name="D-LINK_BC0F9A_NIUFibra" manufacturer="D-LINK_BC0F9A_NIUFibra" oui="BC0F9A" productClass="Router" objectModelDefinitions="InternetGatewayDevice:1.14" description="" setNotification="true" setAccessList="true" protocolType="TR069">
    <supportedRPCMethods>DeleteObject</supportedRPCMethods>
    <supportedRPCMethods>GetParameterNames</supportedRPCMethods>
    <supportedRPCMethods>GetQueuedTransfers</supportedRPCMethods>
    <supportedRPCMethods>CancelTransfer</supportedRPCMethods>
    <supportedRPCMethods>GetParameterAttributes</supportedRPCMethods>
    <supportedRPCMethods>Upload</supportedRPCMethods>
    <supportedRPCMethods>AddObject</supportedRPCMethods>
    <supportedRPCMethods>GetParameterValues</supportedRPCMethods>
    <supportedRPCMethods>Reboot</supportedRPCMethods>
    <supportedRPCMethods>SetParameterAttributes</supportedRPCMethods>
    <supportedRPCMethods>GetRPCMethods</supportedRPCMethods>
    <supportedRPCMethods>GetAllQueuedTransfers</supportedRPCMethods>
    <supportedRPCMethods>ScheduleInform</supportedRPCMethods>
    <supportedRPCMethods>SetParameterValues</supportedRPCMethods>
    <supportedRPCMethods>Download</supportedRPCMethods>
    <supportedRPCMethods>FactoryReset</supportedRPCMethods>
    <options discoveryAlgorithmType="ALL_AT_ONCE" dashboardDevicePollTime="10" reloadOnFactoryReset="NEVER" collectConnectedDevices="false" addObjectBackfill="true" discoveryRetry="0" simpleDiscoveryRetry="3" simpleDiscoveryEnabled="false"/>
    <deviceServiceConfigurations name="Device Log">
        <scriptDefinition name="D-LINK_BC0F9A_NIUFibras: Device Log" purpose="Device service configuration" tags="null" scriptParameters="[]">
            <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var deviceId = scriptParameters.deviceId;
var response = dsc.getDeviceParameterLogs(deviceId);

response;
</javaScriptCode>
        </scriptDefinition>
    </deviceServiceConfigurations>
    <deviceServiceConfigurations name="TR-69 Config">
        <scriptDefinition name="D-LINK_BC0F9A_NIUFibras: TR-69 Config" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="WiFi 1">
        <scriptDefinition name="D-LINK_BC0F9A_NIUFibras: WiFi 1" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="DHCP">
        <scriptDefinition name="D-LINK_BC0F9A_NIUFibras: DHCP" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="WiFi 2">
        <scriptDefinition name="D-LINK_BC0F9A_NIUFibras: WiFi 2" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceLogParameters name="Device Log 1" parameterName="InternetGatewayDevice.DeviceInfo.DeviceLog"/>
    <dataComposers name="Bytes Sent">
        <scriptDefinition name="D-LINK_BC0F9A_NIUFibras: Bytes Sent" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <dataComposers name="Bytes Received">
        <scriptDefinition name="D-LINK_BC0F9A_NIUFibras: Bytes Received" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
            <scriptDefinition name="D-LINK_BC0F9A_NIUFibras:##dashboard.device_info.name##" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
        <dashboardPanelScript name="##dashboard.connected_devices_topology.name##" scriptType="DASHBOARD_SCRIPT">
            <scriptDefinition name="D-LINK_BC0F9A_NIUFibras:##dashboard.connected_devices_topology.name##" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    { name: "SignalStrength", label: "Signal Strength", cpeParameterName: "Device.X_Incognito.ConnectedDevices.Host.{i}.SignalStrength" },
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
        <dashboardPanelScript name="##dashboard.tr069_config.name##" scriptType="DASHBOARD_SCRIPT">
            <scriptDefinition name="D-LINK_BC0F9A_NIUFibras:##dashboard.tr069_config.name##" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
        <widgets name="Connected Devices" type="CONNECTED_DEVICES" description="Connected Devices" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">three-desktops</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">22</value>
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
        <widgets name="WiFi 1" type="SERVICE_CONFIGURATION" description="Wireless Network" stale="true">
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 1</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="DHCP" type="SERVICE_CONFIGURATION" description="Device DHCP" stale="true">
            <configuration>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">DHCP</value>
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
        <widgets name="WiFi 2" type="SERVICE_CONFIGURATION" description="Wireless Network" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">wifi-signal</value>
                </entry>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 2</value>
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
        <widgets name="Diagnostics" type="DIAGNOSTICS" description="Device Diagnostics" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">stethoscope</value>
                </entry>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">18</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">20</value>
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
        <allowAllGroups>TRUE</allowAllGroups>
        <config/>
    </dashboards>
    <dashboardPanels>
        <dashboardPanel name="Broadband Speed Test" panelType="PANEL_DASHBOARD_BROADBAND_SPEED">
            <configuration>{"diagnosticsConfig":[{"id":"Download Diagnostics","subType":"DOWNLOADSPEED","diagnosticParameters":[{"name":"InternetGatewayDevice.DownloadDiagnostics.DownloadURL","value":"http://35.208.72.200:8080/static/100mb.bin"},{"name":"InternetGatewayDevice.DownloadDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.DownloadDiagnostics.DSCP","value":""},{"name":"InternetGatewayDevice.DownloadDiagnostics.EthernetPriority","value":""}]},{"id":"Upload Diagnostics","subType":"UPLOADSPEED","diagnosticParameters":[{"name":"InternetGatewayDevice.UploadDiagnostics.EthernetPriority","value":""},{"name":"InternetGatewayDevice.UploadDiagnostics.UploadURL","value":"http://35.208.72.200:8081/test.file"},{"name":"InternetGatewayDevice.UploadDiagnostics.DSCP","value":""},{"name":"InternetGatewayDevice.UploadDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.UploadDiagnostics.TestFileLength","value":"1000"}]}],"tabName":"03250d85-029a-0cf6-e001-50851d216d1f","InternetGatewayDevice.DownloadDiagnostics.DownloadURL":"http://35.208.72.200:8080/static/100mb.bin","InternetGatewayDevice.DownloadDiagnostics.Interface":"","InternetGatewayDevice.DownloadDiagnostics.DSCP":"","InternetGatewayDevice.DownloadDiagnostics.EthernetPriority":"","InternetGatewayDevice.UploadDiagnostics.EthernetPriority":"","InternetGatewayDevice.UploadDiagnostics.UploadURL":"http://35.208.72.200:8081/test.file","InternetGatewayDevice.UploadDiagnostics.DSCP":"","InternetGatewayDevice.UploadDiagnostics.Interface":"","InternetGatewayDevice.UploadDiagnostics.TestFileLength":"1000"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.admin_actions.name##" panelType="PANEL_DEVICE_OPERATIONS_ADMIN">
            <configuration>{"actionsConfig":[{"id":"ManageOperation","text":"Manage Operations","url":"#devices/{deviceId}/active-operations","order":1,"visible":true},{"id":"ObjectStructParameter","text":"Manage Object Structure &amp; Parameters","url":"#devices/{deviceId}/parameters","order":2,"visible":true},{"id":"ManageGroupings","text":"Manage Groupings","url":"#devices/{deviceId}/device-groups","order":3,"visible":true},{"id":"ViewDeviceInfo","text":"View Device Information","url":"#devices/{deviceId}/device","order":4,"visible":true},{"id":"DeviceWorkbench","text":"Device Workbench","url":"#devices/{deviceId}/workbench","order":5,"visible":true},{"id":"ComplianceTestSuite","text":"Run Compliance Test Suite","url":"#devices/{deviceId}/execute-device-compliance-suite","order":6,"visible":true},{"id":"PerformActions","text":"Perform Actions","url":"#devices/{deviceId}/devicemodel/{deviceModelId}/device_actions","order":7,"visible":true},{"id":"PerformDiagnostics","text":"Perform Diagnostics","url":"#devices/{deviceId}/devicemodel/{deviceModelId}/diagnostics","order":8,"visible":true}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.common_issues.name##" panelType="PANEL_DEVICE_OPERATIONS_ISSUES">
            <configuration>{"actionsConfig":[{"order":0,"include":true,"text":"Incognito Support","url":"https://support.incognito.com/"}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.device_info.name##" panelType="PANEL_DASHBOARD_DEVICE_INFO">
            <configuration>{"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"##dashboard.device_info.name##","sourceIdSet":[]},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"panelType":"PANEL_STATUS_ONLINE"}}]},"buttons":{"handlers":[{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"readOnly":true}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.ipping.name##" panelType="PANEL_DASHBOARD_IPPING">
            <configuration>{"buttons":{"handlers":[{"text":"Run","handler":"runDiagnostics","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"POST"},"visible":true,"tab":null},{"text":"Cancel","handler":"cancelDiagnostics","endpoint":{"url":"/deviceoperations/cancellation","verb":"POST"},"visible":false,"tab":null}]},"diagnosticsConfig":[{"id":"IP Ping Diagnostics","subType":"IPPING","diagnosticParameters":[{"name":"InternetGatewayDevice.IPPingDiagnostics.Interface","value":null},{"name":"InternetGatewayDevice.IPPingDiagnostics.Host","value":null},{"name":"InternetGatewayDevice.IPPingDiagnostics.DSCP","value":null},{"name":"InternetGatewayDevice.IPPingDiagnostics.DataBlockSize","value":null},{"name":"InternetGatewayDevice.IPPingDiagnostics.Timeout","value":null},{"name":"InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions","value":null}]}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.sync_status.name##" panelType="PANEL_STATUS_SYNC">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.traceroute.name##" panelType="PANEL_DASHBOARD_TRACEROUTE">
            <configuration>{"buttons":{"handlers":[{"text":"Run","handler":"runDiagnostics","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"POST"},"visible":true,"tab":null},{"text":"Cancel","handler":"cancelDiagnostics","endpoint":{"url":"/deviceoperations/cancellation","verb":"POST"},"visible":false,"tab":null}]},"diagnosticsConfig":[{"id":"TraceRoute Diagnostics","subType":"TRACEROUTE","diagnosticParameters":[{"name":"InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount","value":null},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.Host","value":null},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.Timeout","value":null},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries","value":null},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.Interface","value":null},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize","value":null},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.DSCP","value":null}]}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.device_actions.name##" panelType="PANEL_DEVICE_OPERATIONS_ACTIONS">
            <configuration>{"actionsConfig":[],"moreButton":{"handlers":[{"text":"##dashboard.more_device_actions##","handler":"showMoreActions","visible":true}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.failed_operations.name##" panelType="PANEL_STATUS_OPERATIONS_FAILED">
            <configuration>{"links":{"#panelStatusOperationsFailed":{"url":"#devices/{deviceId}/failed-operations"}},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"rules":{"type":"numeric","threshold":"NONE"},"unit":null}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.up_time.name##" panelType="PANEL_STATUS_UPTIME">
            <configuration>{"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.DeviceInfo.UpTime","sourceIdSet":[]},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"duration":{"enable":true,"unit":"seconds"}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.online.name##" panelType="PANEL_STATUS_ONLINE">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.active_operations.name##" panelType="PANEL_STATUS_OPERATIONS_ACTIVE">
            <configuration>{"links":{"#panelStatusOperationsActive":{"url":"#devices/{deviceId}/active-operations"}},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"rules":{"type":"numeric","threshold":"NONE"},"unit":null}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.connected_devices.name##" panelType="PANEL_STATUS_CONNECTED">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"rules":{"type":"numeric","threshold":"NONE"}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.last_seen.name##" panelType="PANEL_STATUS_LASTSEEN">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"duration":{"enable":false,"unit":null}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.broadband_speed_hist.name##" panelType="PANEL_DASHBOARD_BROADBAND_HISTORICAL">
            <configuration>{"buttons":{"handlers":[{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"tableConfig":{"searchName":"PANEL_DASHBOARD_BROADBAND_HISTORICAL","title":"Historic Broadband Speed Test Results","searchParams":{"tableName":"DIAGNOSTIC_RESULT_SUMMARY","url":"/devices/{deviceId}/diagnostics/speedtest","q":"PINGTESTDATE is null","pageSize":20,"orderBy":"LASTMODIFIED","ascending":false},"columns":[{"name":"time","field":"lastModified","label":"Time","align":"left","dataType":"DATETIME","fieldFormat":"hh:mma, dd MMM yyyy"},{"name":"dload","field":"downloadSpeed","label":"Download Speed (Mbps)","align":"center","dataType":"MBYTES","fieldFormat":"%.1f"},{"name":"uload","field":"uploadSpeed","label":"Upload Speed (Mbps)","align":"center","dataType":"MBYTES","fieldFormat":"%.1f"}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.session_info.name##" panelType="PANEL_DASHBOARD_SESSION_INFO">
            <configuration>{"buttons":{"handlers":[{"text":"Initiate Session","handler":"initiateSession","endpoint":{"url":"/devices/{deviceId}/connectionrequest?async=true","verb":"POST"},"visible":true,"tab":null}]},"websockets":{"ws":"/devices/{deviceId}?X-Atmosphere-tracking-id=0&amp;X-Cache-Date=0&amp;Content-Type=application/json&amp;X-atmo-protocol=true","handlers":[{"type":"TR69_INFORM_EVENT"},{"type":"TR69_SESSION_EVENT"},{"type":"TR69_CONNECTION_REQUEST_EVENT"}]},"readOnly":false}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.tr069_config.name##" panelType="PANEL_DASHBOARD_TR069_CONFIG">
            <configuration>{"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"##dashboard.tr069_config.name##","sourceIdSet":[]},"buttons":{"handlers":[{"text":"Save","handler":"saveServiceConfigParameters","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"POST"},"visible":true,"tab":null},{"text":"Cancel","handler":"cancel","endpoint":{"url":"/deviceoperations/cancellation","verb":"POST"},"visible":false,"tab":null},{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"readOnly":false}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.connected_devices_topology.name##" panelType="PANEL_DASHBOARD_CONNECTED_DEVICES">
            <configuration>{"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"##dashboard.connected_devices_topology.name##","sourceIdSet":[]},"buttons":{"handlers":[{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"readOnly":false}</configuration>
        </dashboardPanel>
    </dashboardPanels>
    <dashboardLayout>{"version":"1.2","children":[{"type":"COLUMN_LEFT","order":0,"hasPanelChildren":false,"children":[{"name":"##dashboard.layout.region.device_ident##","type":"REGION_DEVICE_IDENTIFIER","order":0,"hasPanelChildren":false,"children":[{"name":"PANEL_COMMON_DEVICE_IDENTIFIER","type":"PANEL_COMMON_DEVICE_IDENTIFIER","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.customer_ident##","type":"REGION_CUSTOMER_IDENTIIFIER","order":1,"hasPanelChildren":true,"children":[{"name":"PANEL_COMMON_CUSTOMER_IDENTIFIER","type":"PANEL_COMMON_CUSTOMER_IDENTIFIER","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.images##","type":"REGION_DEVICE_IMAGES","order":2,"hasPanelChildren":true,"children":[{"name":"PANEL_COMMON_DEVICE_IMAGES","type":"PANEL_COMMON_DEVICE_IMAGES","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.operations##","type":"REGION_DEVICE_OPERATIONS","order":3,"hasPanelChildren":true,"children":[{"name":"##dashboard.device_actions.name##","type":"PANEL_DEVICE_OPERATIONS_ACTIONS","order":0,"hasPanelChildren":false},{"name":"##dashboard.common_issues.name##","type":"PANEL_DEVICE_OPERATIONS_ISSUES","order":1,"hasPanelChildren":false},{"name":"##dashboard.admin_actions.name##","type":"PANEL_DEVICE_OPERATIONS_ADMIN","order":2,"hasPanelChildren":false}]}]},{"type":"COLUMN_RIGHT","order":1,"hasPanelChildren":false,"children":[{"name":"##dashboard.layout.region.status##","type":"REGION_STATUS","order":0,"hasPanelChildren":true,"children":[{"name":"##dashboard.online.name##","type":"PANEL_STATUS_ONLINE","order":0,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.sync_status.name##","type":"PANEL_STATUS_SYNC","order":1,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.connected_devices.name##","type":"PANEL_STATUS_CONNECTED","order":2,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.active_operations.name##","type":"PANEL_STATUS_OPERATIONS_ACTIVE","order":3,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.failed_operations.name##","type":"PANEL_STATUS_OPERATIONS_FAILED","order":4,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.last_seen.name##","type":"PANEL_STATUS_LASTSEEN","order":5,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.up_time.name##","type":"PANEL_STATUS_UPTIME","order":6,"hasPanelChildren":false,"visible":true}]},{"name":"##dashboard.layout.region.csr_call_log##","type":"REGION_CSR_CALL_INFO","order":1,"hasPanelChildren":true,"children":[{"name":"##dashboard.csr_call_info.name##","type":"PANEL_COMMON_CSR_CALL_INFO","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.dashboards##","type":"REGION_DASHBOARDS","order":2,"hasPanelChildren":false,"children":[{"name":"##dashboard.tab.overview##","type":"TAB_DASHBOARD","order":0,"hasPanelChildren":true,"visible":true,"children":[{"name":"##dashboard.device_info.name##","type":"PANEL_DASHBOARD_DEVICE_INFO","order":0,"hasPanelChildren":false,"size":{"h":1,"v":1}},{"name":"Broadband Speed Test","type":"PANEL_DASHBOARD_BROADBAND_SPEED","order":1,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"##dashboard.broadband_speed_hist.name##","type":"PANEL_DASHBOARD_BROADBAND_HISTORICAL","order":2,"hasPanelChildren":false,"size":{"h":1,"v":1}},{"name":"##dashboard.session_info.name##","type":"PANEL_DASHBOARD_SESSION_INFO","order":3,"hasPanelChildren":false,"size":{"h":1,"v":1}}]},{"name":"##dashboard.tab.topology##","type":"TAB_DASHBOARD","order":1,"hasPanelChildren":true,"visible":false,"children":[{"name":"##dashboard.connected_devices_topology.name##","type":"PANEL_DASHBOARD_CONNECTED_DEVICES","order":0,"hasPanelChildren":false,"size":{"h":2,"v":1}}]},{"name":"##dashboard.tab.diagnostics##","type":"TAB_DASHBOARD","order":2,"hasPanelChildren":true,"visible":false,"children":[{"name":"##dashboard.tr069_config.name##","type":"PANEL_DASHBOARD_TR069_CONFIG","order":0,"hasPanelChildren":false,"size":{"h":1,"v":1}},{"name":"##dashboard.ipping.name##","type":"PANEL_DASHBOARD_IPPING","order":1,"hasPanelChildren":false,"size":{"h":1,"v":1}},{"name":"##dashboard.traceroute.name##","type":"PANEL_DASHBOARD_TRACEROUTE","order":2,"hasPanelChildren":false,"size":{"h":1,"v":1}}]}]}]}]}</dashboardLayout>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DNSServers" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DNSServers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.ErrorsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.ErrorsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.MemoryStatus.Total" elementDefinition="InternetGatewayDevice.DeviceInfo.MemoryStatus.Total" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.EOMTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.EOMTime" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.DuplexMode" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.DuplexMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANInterfaces.LANEthernetInterfaceConfig.{i}.Name" elementDefinition="InternetGatewayDevice.LANInterfaces.LANEthernetInterfaceConfig.{i}.Name" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANInterfaces.LANEthernetInterfaceConfig.{i}.Name" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.BOMTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.BOMTime" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.Features" elementDefinition="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.Features" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MACAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MACAddress" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.UploadDiagnostics.DSCP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.MaxMarkingEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.MaxMarkingEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.DeviceLog" elementDefinition="InternetGatewayDevice.DeviceInfo.DeviceLog" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MACAddressControlEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MACAddressControlEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNUsername" elementDefinition="InternetGatewayDevice.ManagementServer.STUNUsername" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.Layer2Interface" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.Layer2Interface" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.Interface" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WMMSupported" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WMMSupported" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_DLINK_FirewallEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_DLINK_FirewallEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_DLINK_FirewallEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DNSServers" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DNSServers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.AdditionalHardwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.AdditionalHardwareVersion" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UploadTransports" elementDefinition="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UploadTransports" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.Username" elementDefinition="InternetGatewayDevice.ManagementServer.Username" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.PeriodicInformInterval" elementDefinition="InternetGatewayDevice.ManagementServer.PeriodicInformInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDeviceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDeviceNumberOfEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.ClientID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.ClientID" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.RouteProtocolRx" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.RouteProtocolRx" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.DownloadTransports" elementDefinition="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.DownloadTransports" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetUnicastPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetUnicastPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKeyIndex" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKeyIndex" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.AdditionalSoftwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.AdditionalSoftwareVersion" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANInterfaces.LANEthernetInterfaceConfig.{i}.MACAddress" elementDefinition="InternetGatewayDevice.LANInterfaces.LANEthernetInterfaceConfig.{i}.MACAddress" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANInterfaces.LANEthernetInterfaceConfig.{i}.MACAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.SuccessCount" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.SuccessCount" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.DataBlockSize" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.DataBlockSize" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.VLANIDMarkOverride" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.VLANIDMarkOverride" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddress" elementDefinition="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANConfigSecurity.ConfigPassword" elementDefinition="InternetGatewayDevice.LANConfigSecurity.ConfigPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.DiscardPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.DiscardPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.DiscardPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.DiscardPacketsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.HardwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.HardwareVersion" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPExternalServerIPAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPExternalServerIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPExternalServerIPAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.User.{i}.Password" elementDefinition="InternetGatewayDevice.User.{i}.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.MaximumResponseTime" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.MaximumResponseTime" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.STAWMMParameter.{i}.ECWMax" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.STAWMMParameter.{i}.ECWMax" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.RemoteAccess.Protocol" elementDefinition="InternetGatewayDevice.UserInterface.RemoteAccess.Protocol" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_DLINK_Redirect.Rule.{i}.Description" elementDefinition="InternetGatewayDevice.Services.X_DLINK_Redirect.Rule.{i}.Description" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_DLINK_Redirect.Rule.{i}.Description" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.LocalTimeZoneName" elementDefinition="InternetGatewayDevice.Time.LocalTimeZoneName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterStatus" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterStatus" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ExternalIPAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ExternalIPAddress" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.SoftwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.SoftwareVersion" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.OperationalDataTransmitRates" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.OperationalDataTransmitRates" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.RemoteAccess.Enable" elementDefinition="InternetGatewayDevice.UserInterface.RemoteAccess.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceived" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.DaylightSavingsUsed" elementDefinition="InternetGatewayDevice.Time.DaylightSavingsUsed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DomainName" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DomainName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.VLANIDFilter" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.VLANIDFilter" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Type" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Type" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PossibleChannels" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PossibleChannels" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnectionNumberOfEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MaxBitRate" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnicastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnicastPacketsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBytesSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBytesSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BroadcastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BroadcastPacketsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalAssociations" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalAssociations" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.Timeout" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.Timeout" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.URL" elementDefinition="InternetGatewayDevice.ManagementServer.URL" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.MulticastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.MulticastPacketsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnicastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnicastPacketsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.TransportType" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.TransportType" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPAuthenticationProtocol" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPAuthenticationProtocol" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPowerSupported" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPowerSupported" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNServerPort" elementDefinition="InternetGatewayDevice.ManagementServer.STUNServerPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeName" elementDefinition="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPEncryptionLevel" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPEncryptionLevel" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.APWMMParameter.{i}.ECWMin" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.APWMMParameter.{i}.ECWMin" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.UploadURL" elementDefinition="InternetGatewayDevice.UploadDiagnostics.UploadURL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.X_DLINK_UpdateInterval" elementDefinition="InternetGatewayDevice.Time.X_DLINK_UpdateInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Time.X_DLINK_UpdateInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicDataTransmitRates" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicDataTransmitRates" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TestFileLength" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TestFileLength" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDeviceNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDeviceNumberOfEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ConnectionStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ConnectionStatus" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKey.{i}.WEPKey" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKey.{i}.WEPKey" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MACAddressControlEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MACAddressControlEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoRateFallBackEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoRateFallBackEnabled" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPLeaseTime" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPLeaseTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingKey" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingKey" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DNSEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DNSEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Status" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Status" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnectionRequestUsername" elementDefinition="InternetGatewayDevice.ManagementServer.ConnectionRequestUsername" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.AverageResponseTime" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.AverageResponseTime" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingInterface" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingInterface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.Enable" elementDefinition="InternetGatewayDevice.Time.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterKey" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterKey" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.FilterNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.FilterNumberOfEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_StandardSupported" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_StandardSupported" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_StandardSupported" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsReceived" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BeaconType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BeaconType" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceConfig.PersistentData" elementDefinition="InternetGatewayDevice.DeviceConfig.PersistentData" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.UploadDiagnostics.DiagnosticsState" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesSent" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_DLINK_BytesReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_DLINK_BytesReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_DLINK_BytesReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Status" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Status" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterBridgeReference" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterBridgeReference" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.RadioEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.RadioEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DSCP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.EnableCWMP" elementDefinition="InternetGatewayDevice.ManagementServer.EnableCWMP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.MulticastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.MulticastPacketsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeKey" elementDefinition="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeKey" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Password" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.DiscardPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.DiscardPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicAuthenticationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicAuthenticationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPServerEnableIPv6" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPServerEnableIPv6" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPServerEnableIPv6" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.SupportedDataModelNumberOfEntries" elementDefinition="InternetGatewayDevice.DeviceInfo.SupportedDataModelNumberOfEntries" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesSent" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.DSCP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesReceived" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.AdmitOnlyVLANTagged" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.AdmitOnlyVLANTagged" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceConfig.ConfigFile" elementDefinition="InternetGatewayDevice.DeviceConfig.ConfigFile" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANUSBInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANUSBInterfaceNumberOfEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.AssociatedDeviceMACAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.AssociatedDeviceMACAddress" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnectionNumberOfEntries" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ProductClass" elementDefinition="InternetGatewayDevice.DeviceInfo.ProductClass" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesReceived" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPoEServiceName" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPoEServiceName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Name" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Name" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.DefaultConnectionService" elementDefinition="InternetGatewayDevice.Layer3Forwarding.DefaultConnectionService" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.GatewayIPAddress" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.GatewayIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.MACAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.MACAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.LocalTimeZone" elementDefinition="InternetGatewayDevice.Time.LocalTimeZone" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ParameterKey" elementDefinition="InternetGatewayDevice.ManagementServer.ParameterKey" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.X_DLINK_CurrDuplex" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.X_DLINK_CurrDuplex" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.X_DLINK_CurrDuplex" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BSSID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BSSID" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MaxAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MaxAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsSent" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_DLINK_ParentalControl.Enable" elementDefinition="InternetGatewayDevice.Services.X_DLINK_ParentalControl.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_DLINK_ParentalControl.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TotalBytesSent" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TotalBytesSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBytesReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBytesReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.PhysicalLinkStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.PhysicalLinkStatus" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.URL" elementDefinition="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.URL" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.URN" elementDefinition="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.URN" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.UpTime" elementDefinition="InternetGatewayDevice.DeviceInfo.UpTime" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.Host" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.Host" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterInterface" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterInterface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.ExclusivityOrder" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.ExclusivityOrder" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.MarkingNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.MarkingNumberOfEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.UpgradesManaged" elementDefinition="InternetGatewayDevice.ManagementServer.UpgradesManaged" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.MulticastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.MulticastPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.SpecVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.SpecVersion" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_DLINK_CRCErroredPackets" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_DLINK_CRCErroredPackets" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_DLINK_CRCErroredPackets" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Standard" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Standard" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.RemoteAccess.Port" elementDefinition="InternetGatewayDevice.UserInterface.RemoteAccess.Port" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.MaxBridgeEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.MaxBridgeEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.Host" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.Host" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Name" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANWLANConfigurationNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANWLANConfigurationNumberOfEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.APWMMParameter.{i}.ECWMax" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.APWMMParameter.{i}.ECWMax" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.AssociatedDeviceAuthenticationState" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.AssociatedDeviceAuthenticationState" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.ROMTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.ROMTime" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.EnabledForInternet" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.EnabledForInternet" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigMethodsEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigMethodsEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PossibleConnectionTypes" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PossibleConnectionTypes" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_DLINK_ALG.RTSPEnable" elementDefinition="InternetGatewayDevice.Services.X_DLINK_ALG.RTSPEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_DLINK_ALG.RTSPEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNPassword" elementDefinition="InternetGatewayDevice.ManagementServer.STUNPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ConnectionTrigger" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ConnectionTrigger" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Reset" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Reset" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ModemFirmwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.ModemFirmwareVersion" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_DLINK_Redirect.Enable" elementDefinition="InternetGatewayDevice.Services.X_DLINK_Redirect.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_DLINK_Redirect.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetMulticastPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetMulticastPacketsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.CWMPRetryIntervalMultiplier" elementDefinition="InternetGatewayDevice.ManagementServer.CWMPRetryIntervalMultiplier" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnicastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnicastPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.BroadcastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.BroadcastPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.InterfaceType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.InterfaceType" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.BroadcastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.BroadcastPacketsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACAddressFilterList" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACAddressFilterList" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadURL" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DownloadURL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANInterfaces.LANUSBInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANInterfaces.LANUSBInterfaceNumberOfEntries" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBroadcastPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBroadcastPacketsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.DiscardPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.DiscardPacketsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterfaceNumberOfEntries" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPower" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPower" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ConnectionType" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.ConnectionType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNEnable" elementDefinition="InternetGatewayDevice.ManagementServer.STUNEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsSent" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetErrorsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetErrorsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.X_WANReferenceList" elementDefinition="InternetGatewayDevice.ManagementServer.X_WANReferenceList" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.X_WANReferenceList" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPLeaseTimeIPv6" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPLeaseTimeIPv6" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPLeaseTimeIPv6" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPRouters" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPRouters" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_DLINK_Redirect.Rule.{i}.Enable" elementDefinition="InternetGatewayDevice.Services.X_DLINK_Redirect.Rule.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_DLINK_Redirect.Rule.{i}.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterEnable" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPacketsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnicastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnicastPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1UpstreamMaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1UpstreamMaxBitRate" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_MaxAddressIPv6" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_MaxAddressIPv6" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_MaxAddressIPv6" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAEncryptionModes" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAEncryptionModes" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalBytesSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalBytesSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPStaticAddressNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPStaticAddressNumberOfEntries" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.EthertypeFilterExclude" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.EthertypeFilterExclude" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.ReservedAddresses" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.ReservedAddresses" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAAuthenticationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAAuthenticationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.VendorClassID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.VendorClassID" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.X_DLINK_CurrBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.X_DLINK_CurrBitRate" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.X_DLINK_CurrBitRate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.APWMMParameter.{i}.TXOP" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.APWMMParameter.{i}.TXOP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.EthernetLinkStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.EthernetLinkStatus" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnectionRequestURL" elementDefinition="InternetGatewayDevice.ManagementServer.ConnectionRequestURL" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.Active" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.Active" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.Interface" elementDefinition="InternetGatewayDevice.UploadDiagnostics.Interface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_COM_IgmpSnoopingConfig.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_COM_IgmpSnoopingConfig.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_COM_IgmpSnoopingConfig.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenResponseTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TCPOpenResponseTime" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.CurrentLocalTime" elementDefinition="InternetGatewayDevice.Time.CurrentLocalTime" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_OperatingChannelBandwidth" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_OperatingChannelBandwidth" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_OperatingChannelBandwidth" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerConfigurable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerConfigurable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.NATEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.NATEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.DestIPAddress" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.DestIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANInterfaces.LANWLANConfigurationNumberOfEntries" elementDefinition="InternetGatewayDevice.LANInterfaces.LANWLANConfigurationNumberOfEntries" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.MaxQBridgeEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.MaxQBridgeEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.Status" elementDefinition="InternetGatewayDevice.Time.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.X_DLINK_CurrDuplex" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.X_DLINK_CurrDuplex" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.X_DLINK_CurrDuplex" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeStandard" elementDefinition="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeStandard" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Status" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Status" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.EthernetPriorityOverride" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.EthernetPriorityOverride" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ManageableDeviceNumberOfEntries" elementDefinition="InternetGatewayDevice.ManagementServer.ManageableDeviceNumberOfEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BeaconAdvertisementEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BeaconAdvertisementEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_GuestZone_PossibleEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_GuestZone_PossibleEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_GuestZone_PossibleEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.DSCP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserNumberOfEntries" elementDefinition="InternetGatewayDevice.UserNumberOfEntries" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigMethodsSupported" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigMethodsSupported" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.SourceSubnetMask" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.SourceSubnetMask" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_DLINK_ParentalControl.URLFilter.RuleNumberOfEntries" elementDefinition="InternetGatewayDevice.Services.X_DLINK_ParentalControl.URLFilter.RuleNumberOfEntries" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_DLINK_ParentalControl.URLFilter.RuleNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MaxBitRate" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.MACAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.MACAddress" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPSKFailures" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPSKFailures" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingBridgeReference" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingBridgeReference" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.HostName" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.HostName" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.X_DLINK_CurrBitRate" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.X_DLINK_CurrBitRate" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.X_DLINK_CurrBitRate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.NTPServer5" elementDefinition="InternetGatewayDevice.Time.NTPServer5" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ManufacturerOUI" elementDefinition="InternetGatewayDevice.DeviceInfo.ManufacturerOUI" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.NTPServer1" elementDefinition="InternetGatewayDevice.Time.NTPServer1" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.ROMTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.ROMTime" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.NTPServer2" elementDefinition="InternetGatewayDevice.Time.NTPServer2" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.NTPServer3" elementDefinition="InternetGatewayDevice.Time.NTPServer3" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.WANAccessType" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.WANAccessType" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.NTPServer4" elementDefinition="InternetGatewayDevice.Time.NTPServer4" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_COM_IgmpSnoopingConfig.SourceEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_COM_IgmpSnoopingConfig.SourceEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_COM_IgmpSnoopingConfig.SourceEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.StaticRoute" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.StaticRoute" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPSupportedmodesIPv6" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPSupportedmodesIPv6" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPSupportedmodesIPv6" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetDiscardPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetDiscardPacketsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBroadcastPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetBroadcastPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_DLINK_RSSI" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_DLINK_RSSI" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_DLINK_RSSI" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.MaxMRUSize" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.MaxMRUSize" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.MulticastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.MulticastPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iAuthenticationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iAuthenticationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.NATDetected" elementDefinition="InternetGatewayDevice.ManagementServer.NATDetected" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.ForwardNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer3Forwarding.ForwardNumberOfEntries" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnectionRequestPassword" elementDefinition="InternetGatewayDevice.ManagementServer.ConnectionRequestPassword" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnknownProtoPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnknownProtoPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.AvailableInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.AvailableInterfaceNumberOfEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PossibleDataTransmitRates" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PossibleDataTransmitRates" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACAddressFilterExclude" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACAddressFilterExclude" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MACAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MACAddress" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.RemoteAccess.SupportedProtocols" elementDefinition="InternetGatewayDevice.UserInterface.RemoteAccess.SupportedProtocols" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_AllowHighChannels" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_AllowHighChannels" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_AllowHighChannels" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANInterfaces.LANEthernetInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANInterfaces.LANEthernetInterfaceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenRequestTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TCPOpenRequestTime" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.InterfaceType" elementDefinition="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.InterfaceType" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeStatus" elementDefinition="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeStatus" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelRefreshPeriod" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelRefreshPeriod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelRefreshPeriod" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.MaxFilterEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.MaxFilterEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.AssociatedDeviceIPAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.AssociatedDeviceIPAddress" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceSubnetMask" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceSubnetMask" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UPnP.Device.UPnPIGD" elementDefinition="InternetGatewayDevice.UPnP.Device.UPnPIGD" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_COM_IgmpSnoopingConfig.Mode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_COM_IgmpSnoopingConfig.Mode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_COM_IgmpSnoopingConfig.Mode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACAddressFilterExclude" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACAddressFilterExclude" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.ErrorsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.ErrorsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_DLINK_ParentalControl.Status" elementDefinition="InternetGatewayDevice.Services.X_DLINK_ParentalControl.Status" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_DLINK_ParentalControl.Status" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsReceived" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSIDAdvertisementEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSIDAdvertisementEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.BOMTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.BOMTime" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.RegulatoryDomain" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.RegulatoryDomain" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.SourceIPAddress" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.SourceIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.VLANIDUntag" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.VLANIDUntag" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.LeaseTimeRemaining" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.LeaseTimeRemaining" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPoEACName" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPoEACName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_X_DLINK_WPA_Renewal" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_X_DLINK_WPA_Renewal" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_X_DLINK_WPA_Renewal" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.PeriodicInformEnable" elementDefinition="InternetGatewayDevice.ManagementServer.PeriodicInformEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPServerEnablePDIPv6" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPServerEnablePDIPv6" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPServerEnablePDIPv6" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.STAWMMParameter.{i}.TXOP" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.STAWMMParameter.{i}.TXOP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DiagnosticsState" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.EOMTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.EOMTime" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.X_DLINK_CRCErroredPackets" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.X_DLINK_CRCErroredPackets" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.X_DLINK_CRCErroredPackets" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceSummary" elementDefinition="InternetGatewayDevice.DeviceSummary" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BroadcastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BroadcastPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.RSIPAvailable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.RSIPAvailable" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetPacketsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.AvailableInterfaceKey" elementDefinition="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.AvailableInterfaceKey" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.EthernetPriority" elementDefinition="InternetGatewayDevice.UploadDiagnostics.EthernetPriority" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingStatus" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingStatus" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Uptime" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Uptime" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_PreambleType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_PreambleType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_PreambleType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Name" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Name" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.APWMMParameter.{i}.AckPolicy" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.APWMMParameter.{i}.AckPolicy" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetMulticastPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetMulticastPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_DLINK_Uptime" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_DLINK_Uptime" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_DLINK_Uptime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.EthertypeFilterList" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.EthertypeFilterList" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelRefreshEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelRefreshEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelRefreshEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_GuestZone_Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_GuestZone_Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_GuestZone_Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNMaximumKeepAlivePeriod" elementDefinition="InternetGatewayDevice.ManagementServer.STUNMaximumKeepAlivePeriod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.DestSubnetMask" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.DestSubnetMask" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ProcessStatus.CPUUsage" elementDefinition="InternetGatewayDevice.DeviceInfo.ProcessStatus.CPUUsage" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.IdleDisconnectTime" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.IdleDisconnectTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.EthernetPriorityMark" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.EthernetPriorityMark" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.SerialNumber" elementDefinition="InternetGatewayDevice.DeviceInfo.SerialNumber" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.Interface" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.Interface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNServerAddress" elementDefinition="InternetGatewayDevice.ManagementServer.STUNServerAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingEnable" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.UUID" elementDefinition="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.UUID" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.Timeout" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.Timeout" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DNSOverrideAllowed" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DNSOverrideAllowed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeEnable" elementDefinition="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.BridgeEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.Password" elementDefinition="InternetGatewayDevice.ManagementServer.Password" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPLCPEchoRetry" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPLCPEchoRetry" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.ForwardingMetric" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.ForwardingMetric" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PreSharedKey.{i}.PreSharedKey" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PreSharedKey.{i}.PreSharedKey" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.LastConnectionError" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.LastConnectionError" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_IPInterfaceIPv6Address" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_IPInterfaceIPv6Address" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_IPInterfaceIPv6Address" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.Manufacturer" elementDefinition="InternetGatewayDevice.DeviceInfo.Manufacturer" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.DevicePassword" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.DevicePassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.STAWMMParameter.{i}.AIFSN" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.STAWMMParameter.{i}.AIFSN" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.PeriodicInformTime" elementDefinition="InternetGatewayDevice.ManagementServer.PeriodicInformTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPLCPEcho" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPLCPEcho" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.MinimumResponseTime" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.MinimumResponseTime" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceAddressingType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceAddressingType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_FrequencyBand" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_FrequencyBand" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_FrequencyBand" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.X_AcsPeriodicInformInterval" elementDefinition="InternetGatewayDevice.ManagementServer.X_AcsPeriodicInformInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.X_AcsPeriodicInformInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.DefaultConnectionV6Service" elementDefinition="InternetGatewayDevice.Layer3Forwarding.DefaultConnectionV6Service" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Layer3Forwarding.DefaultConnectionV6Service" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicEncryptionModes" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicEncryptionModes" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.STAWMMParameter.{i}.ECWMin" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.STAWMMParameter.{i}.ECWMin" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_BeaconPeriod" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_BeaconPeriod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_BeaconPeriod" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPModeIPv6" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPModeIPv6" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_DHCPModeIPv6" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Username" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Username" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MaxAssociatedClients" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MaxAssociatedClients" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MaxAssociatedClients" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1DownstreamMaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1DownstreamMaxBitRate" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PreSharedKey.{i}.KeyPassphrase" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PreSharedKey.{i}.KeyPassphrase" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceived" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.AliasBasedAddressing" elementDefinition="InternetGatewayDevice.ManagementServer.AliasBasedAddressing" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Channel" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Channel" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetErrorsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetErrorsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.Interface" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.Interface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.User.{i}.Username" elementDefinition="InternetGatewayDevice.User.{i}.Username" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ProvisioningCode" elementDefinition="InternetGatewayDevice.DeviceInfo.ProvisioningCode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PortMappingNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PortMappingNumberOfEntries" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MACAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MACAddress" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_DLINK_PingEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_DLINK_PingEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.X_DLINK_PingEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.EthernetPriority" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.EthernetPriority" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Interface" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Interface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TCPOpenRequestTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TCPOpenRequestTime" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.IPAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.IPAddress" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.VLANID" elementDefinition="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.VLANID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.MemoryStatus.Free" elementDefinition="InternetGatewayDevice.DeviceInfo.MemoryStatus.Free" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalBytesReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalBytesReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.VLANIDMark" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.VLANIDMark" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iEncryptionModes" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iEncryptionModes" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.HostNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.HostNumberOfEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.DuplexMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.DuplexMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.SubnetMask" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.SubnetMask" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnknownProtoPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnknownProtoPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddressNotificationLimit" elementDefinition="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddressNotificationLimit" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.LastDataTransmitRate" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.LastDataTransmitRate" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_MinAddressIPv6" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_MinAddressIPv6" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_DLINK_MinAddressIPv6" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_COM_IPTV.IGMPVersion" elementDefinition="InternetGatewayDevice.Services.X_COM_IPTV.IGMPVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_COM_IPTV.IGMPVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.ResponseTime" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.ResponseTime" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_DLINK_ALG.SIPEnable" elementDefinition="InternetGatewayDevice.Services.X_DLINK_ALG.SIPEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_DLINK_ALG.SIPEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Enable" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_DLINK_BytesSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_DLINK_BytesSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AssociatedDevice.{i}.X_DLINK_BytesSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNMinimumKeepAlivePeriod" elementDefinition="InternetGatewayDevice.ManagementServer.STUNMinimumKeepAlivePeriod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.KeyPassphrase" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.KeyPassphrase" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ModelName" elementDefinition="InternetGatewayDevice.DeviceInfo.ModelName" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceIPAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceIPAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.CWMPRetryMinimumWaitInterval" elementDefinition="InternetGatewayDevice.ManagementServer.CWMPRetryMinimumWaitInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.X_DLINK_Bridgetype" elementDefinition="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.X_DLINK_Bridgetype" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Layer2Bridging.Bridge.{i}.X_DLINK_Bridgetype" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPRelay" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPRelay" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetDiscardPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetDiscardPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACAddressFilterList" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACAddressFilterList" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MinAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MinAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.Description" elementDefinition="InternetGatewayDevice.DeviceInfo.Description" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.InterfaceReference" elementDefinition="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.InterfaceReference" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.RouteHopsNumberOfEntries" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.RouteHopsNumberOfEntries" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPoESessionID" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.PPPoESessionID" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.BridgeNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.BridgeNumberOfEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_OperatingChannelBandwidthAvailable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_OperatingChannelBandwidthAvailable" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_DLINK_OperatingChannelBandwidthAvailable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.MaxDBridgeEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.MaxDBridgeEntries" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetUnknownProtoPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetUnknownProtoPacketsReceived" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.X_DLINK_RU_GetNTPFromDHCP" elementDefinition="InternetGatewayDevice.Time.X_DLINK_RU_GetNTPFromDHCP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Time.X_DLINK_RU_GetNTPFromDHCP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_DLINK_Syslog.Level" elementDefinition="InternetGatewayDevice.DeviceInfo.X_DLINK_Syslog.Level" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_DLINK_Syslog.Level" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Status" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Status" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.AddressSource" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.AddressSource" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WMMEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WMMEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetUnicastPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.Stats.EthernetUnicastPacketsSent" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.DiagnosticsState" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DefaultGateway" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnection.{i}.DefaultGateway" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TCPOpenResponseTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TCPOpenResponseTime" writable="false" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_DLINK_Syslog.Enable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_DLINK_Syslog.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_DLINK_Syslog.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.APWMMParameter.{i}.AIFSN" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.APWMMParameter.{i}.AIFSN" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.FailureCount" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.FailureCount" writable="false" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.DownloadDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="Download Diagnostics" subType="DOWNLOADSPEED">
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.DSCP" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.Interface" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadURL" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.EthernetPriority" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceived"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.BOMTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.EOMTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceived"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.ROMTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenRequestTime"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.IPPingDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="IP Ping Diagnostics" subType="IPPING">
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.Interface" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.Timeout" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.Host" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.DataBlockSize" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.DSCP" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.MaximumResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.SuccessCount"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.MinimumResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.AverageResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.FailureCount"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.TraceRouteDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="TraceRoute Diagnostics" subType="TRACEROUTE">
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.Host" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.Interface" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.DSCP" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.Timeout" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.TraceRouteDiagnostics.ResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.TraceRouteDiagnostics.RouteHopsNumberOfEntries"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.UploadDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="Upload Diagnostics" subType="UPLOADSPEED">
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.EthernetPriority" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.UploadURL" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.Interface" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.TestFileLength" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.DSCP" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.BOMTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.EOMTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.TCPOpenRequestTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.TCPOpenResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.ROMTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.TotalBytesSent"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelNetworkInterfaces isWAN="false" type="Ethernet" name="Ethernet 1" description="network interface definition">
        <properties name="Port Bytes sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.Stats.BytesSent" parameterType="BYTES_SENT"/>
        <properties name="Port Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.Stats.BytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Port Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.Status" parameterType="OTHER"/>
        <properties name="MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.MACAddress" parameterType="MAC_ADDRESS"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 2" description="network interface definition">
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.SSID" parameterType="SSID"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Status" parameterType="OTHER"/>
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.BSSID" parameterType="OTHER"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Enable" parameterType="OTHER"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.TotalBytesSent" parameterType="BYTES_SENT"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="Ethernet" name="Ethernet 4" description="network interface definition">
        <properties name="Port Bytes sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.4.Stats.BytesSent" parameterType="BYTES_SENT"/>
        <properties name="MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.4.MACAddress" parameterType="MAC_ADDRESS"/>
        <properties name="Port Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.4.Stats.BytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Port Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.4.Status" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="Ethernet" name="Ethernet 3" description="network interface definition">
        <properties name="Port Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.3.Stats.BytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.3.MACAddress" parameterType="MAC_ADDRESS"/>
        <properties name="Port Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.3.Status" parameterType="OTHER"/>
        <properties name="Port Bytes sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.3.Stats.BytesSent" parameterType="BYTES_SENT"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="Ethernet" name="Ethernet 2" description="network interface definition">
        <properties name="MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.MACAddress" parameterType="MAC_ADDRESS"/>
        <properties name="Port Bytes sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.Stats.BytesSent" parameterType="BYTES_SENT"/>
        <properties name="Port Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.Status" parameterType="OTHER"/>
        <properties name="Port Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.Stats.BytesReceived" parameterType="BYTES_RECEIVED"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 1" description="network interface definition">
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.TotalBytesSent" parameterType="BYTES_SENT"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Status" parameterType="OTHER"/>
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.BSSID" parameterType="OTHER"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.SSID" parameterType="SSID"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Enable" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
</DeviceModel>
