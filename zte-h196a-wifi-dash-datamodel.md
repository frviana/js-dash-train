<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<DeviceModel name="ZTE_H196A_V9-LAB" manufacturer="ZTE_H196A_V9-LAB" oui="304240" productClass="H196A V9" objectModelDefinitions="InternetGatewayDevice:1.4" description="" setNotification="true" setAccessList="true" protocolType="TR069">
    <supportedRPCMethods>DeleteObject</supportedRPCMethods>
    <supportedRPCMethods>GetParameterNames</supportedRPCMethods>
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
    <deviceServiceConfigurations name="WiFi 1">
        <scriptDefinition name="ZTE_H196A_V9-LAB: WiFi 1" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
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
   // { label: "Password 1", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.1.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    //{ label: "Password 2", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.2.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    //{ label: "Password 3", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.3.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    //{ label: "Password 4", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.WEPKey.4.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    //{ label: "Password", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.PreSharedKey.1.PreSharedKey", group: "WPA" },
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
    <deviceServiceConfigurations name="WiFi 5">
        <scriptDefinition name="ZTE_H196A_V9-LAB: WiFi 5" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
            <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var channelDataType = {
  type: "ENUM", 
  choice:[
    { systemName: "0", friendlyName: "auto" },
    { systemName: "36", friendlyName: "36" },
    { systemName: "56", friendlyName: "56" },
    { systemName: "100", friendlyName: "100" },
    { systemName: "153", friendlyName: "153" },
    { systemName: "157", friendlyName: "157" },
    { systemName: "161", friendlyName: "161" },
    { systemName: "165", friendlyName: "165" }
  ]
};

var channelWidthDataType = {
  type: "ENUM",
  choice:[
    { systemName:"Auto", friendlyName: "Auto"},
    { systemName:"20Hz", friendlyName: "20Hz"},
    { systemName:"40Hz", friendlyName: "40Hz"}
  ]
};

var transmitPowerDataType = {
  type: "ENUM",
  choice:[
    { systemName:"0", friendlyName: "0%"},
    { systemName:"25", friendlyName: "25%"},
    { systemName:"50", friendlyName: "50%"},
    { systemName:"75", friendlyName: "75%"},
    { systemName:"100", friendlyName: "100%"}
  ]
};

var passwordDataType = {
  type: "STRING",
  hidden: true,
  isPassword: true,
  dependencies: {
    securityMode:[
      {
        name: "Disabled"
      },
      {
        name: "WEP-Shared",
        dataType:{
          type: "STRING", 
          min:10, 
          max:10
        }
      },
      {
        name: "WEP-Open",
        dataType:{
          type: "STRING", 
          min:13, 
          max:13
        }
      },
      {
        name: "TKIPEncryption",
        dataType:{
          type: "STRING", 
          min:8, 
          max:63
        }
      },
      {
        name: "AESEncryption",
        dataType:{
          type: "STRING", 
          min:8, 
          max:63
        }
      },
      {
        name: "TKIPandAESEncryption",
        dataType:{
          type: "STRING", 
          min:8, 
          max:63
        }
      }
    ] 
  }
  
};

var conditionalRendering = [
  {
    group: "WEP-Open",
    dependsOnParameter: "securityMode",
    showOnValue: ["WEP-Open"]
  },
  {
    group: "WEP-Shared",
    dependsOnParameter: "securityMode",
    showOnValue: ["WEP-Shared"]
  },
  {
    group: "WPA",
    dependsOnParameter: "securityMode",
    showOnValue: ["TKIPEncryption", "AESEncryption", "TKIPandAESEncryption"]
  },
  {
    group: "Disabled",
    dependsOnParameter: "securityMode",
    showOnValue: ["Disabled"]
  }
];

var data = {
  name: "wifi2",
  label: "WiFi 5Ghz",
  parameters: [
    { name:"ssid", label: "##wifi.ssid##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.SSID" },
    { name:"enabled", label: "##wifi.wifi_enable##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Enable" },
    { name:"broadcastSsid", label: "##wifi.broadcast_ssid##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.BeaconAdvertisementEnabled" },
    { name:"channel", label: "##wifi.channel##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel", dataType: channelDataType },
    /**{ name:"channelWidth",label: "##wifi.channel_width##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.X_000E50_ChannelWidth", dataType: channelWidthDataType },**/
    { name: "transmitPower",label: "##wifi.transmit_power##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.TransmitPower", dataType: transmitPowerDataType },
    { name: "frequency", label: "##wifi.frequency##", description: "Frequency", value:"5GHz",  writable: false },
    { name:"passwordIndex", label: "##wifi.password_index##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.WEPKeyIndex", groups: ["WEP-Open", "WEP-Shared"] },
    { name:"password1", label: "Password 1", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.WEPKey.1.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: passwordDataType, groups: ["WEP-Open", "WEP-Shared"], readCallback: readPassword },
    { label: "Password 2", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.WEPKey.2.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    { label: "Password 3", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.WEPKey.3.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    { label: "Password 4", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.WEPKey.4.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    /*{ name:"password", label: "##wifi.password##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.PreSharedKey.1.KeyPassphrase", group: "WPA", dataType: passwordDataType },*/
    { name:"password", label: "##wifi.password##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.PreSharedKey.1.KeyPassphrase", groups: ["Disabled","WEP-Open", "WEP-Shared", "WPA"], dataType: passwordDataType, readCallback: readPassword },
    { label: "WPA Authentication Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.WPAAuthenticationMode", internalOnly: true },
    { label: "WPA Encryption Modes", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.WPAEncryptionModes", internalOnly: true },
    { label: "Basic Authentication Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.BasicAuthenticationMode", internalOnly: true },
    { label: "Basic Encryption Modes", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.BasicEncryptionModes", internalOnly: true },
    { label: "Beacon Type", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.BeaconType", internalOnly: true },
    { label: "Standard", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Standard", internalOnly: true },
    { name:"mode", label: "Mode", description: "Standard Mode", readCallback: readStandardModeCallback, writable: false },
    { name:"securityMode", label: "##wifi.security_mode##", description: "Security Mode", readCallback: readSecurityModeCallback }
  ],
  styles: {
    definitions:{
      securityMode:{
        eq:[
          { "value":"TKIPEncryption|TKIPandAESEncryption", "style":"threshold-red"},
          { "value":"AESEncryption", "style":"threshold-blue"}
        ]
      },
      channel:{
        lt:[
          { "value":"5", "style":"threshold-blue"}
        ],
        gteq:[
          { "value":"8", "style":"threshold-red"}
        ],
        eq:[
          { "value":"5", "style":"threshold-yellow"}
        ]
      },
      ssid:{
        always: [
          {"style":"threshold-text-red"}
        ]
      },
      password:{
        always: [
          {"style":"threshold-blue"}
        ]
      },
      mode:{
        eq:[
          { "value":"b", "style":"threshold-green"},
          { "value":"b, g, n", "style":"threshold-brown"}
        ]
      }
    },
    container:{
      width:"size1",
      wrapper:"{border:2px solid #cccccc; background-color:#f8f8f8; min-height: 590px}",
      label:"{color:#111111; font-weight:bold; font-family: 'Courier', sans-serif;}",      
      conditionalValues:{
        ssid:"ssid",
        securityMode:"securityMode",
        channel:"channel",
        mode:"mode",
        password:"password"
      }
    }
  }
  
};


var response = dsc.createResponse({
  data: data,
  scriptParameters: scriptParameters,
  customWrite: update,
  conditionalRendering: conditionalRendering,
  collections:null
});

function readPassword(cpeParameters) {
   var parameter = {}; 
  parameter.writable = cpeParameters.password.writable;
  parameter.stale = cpeParameters.password.stale;
  parameter.disabled = false;
  parameter.dataType = passwordDataType;
  if (cpeParameters.BasicEncryptionModes.value == "WEPEncryption") {
    // WEP-Open, WEP-Shared;
    if (typeof cpeParameters.password1 !== 'undefined' &amp;&amp; cpeParameters.password1 !== null) {
      parameter.value = cpeParameters.password1.value;
    }
  } else {
    if (cpeParameters.BeaconType.value == "Basic") {
       parameter.value = null;
    } else {
       if (typeof cpeParameters.password !== 'undefined' &amp;&amp; cpeParameters.password !== null) {
         parameter.value = cpeParameters.password.value;
       }
    }
  }

  return parameter;
}

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
  parameter.value = "b-g-n";//cpeParameters.Standard.value;
  parameter.dataType = {
    type: "ENUM",
    choice:[
      { systemName:"b", friendlyName: "11b Only" },
      { systemName:"g", friendlyName: "11g Only" },
      { systemName:"b, g", friendlyName: "Mixed 11b &amp; 11g" },
      { systemName:"n", friendlyName: "11n Only" },
      { systemName:"b-g-n", friendlyName: "Mixed 11b, 11g &amp; 11n" }
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
    case "ssid": 
          cpeParameters.ssid.updated = true;
          cpeParameters.ssid.value = value;
          break;
    case "channel": 
         // if(value &lt; 0 || value &gt; 165)
         //    throw "Channel number invalid. Must be 36 - 165";
          cpeParameters.channel.value = value;
          cpeParameters.channel.updated = true;
          break;
    case "enabled":
          cpeParameters.enabled.value = value === "true" ? 1 : 0;
          cpeParameters.enabled.updated = true;
          break;
    case "broadcastSsid":
          cpeParameters.broadcastSsid.value = value === "true" ? 1 : 0;
          cpeParameters.broadcastSsid.updated = true;
          break;
    case "Standard":
          cpeParameters.Standard.value = value;
          cpeParameters.Standard.updated = true;
          break;
    case "securityMode":         
          if (value == "Disabled") {
            cpeParameters.BasicAuthenticationMode.value = "None";
            cpeParameters.BasicAuthenticationMode.updated = true;
            cpeParameters.BasicEncryptionModes.value = "None";
            cpeParameters.BasicEncryptionModes.updated = true;
            cpeParameters.BeaconType.value = "Basic";
            cpeParameters.BeaconType.updated = true;
          } else if(value == "WEP-Shared" || value == "WEP-Open") {
            var PasswordIndex = 1;
            
            /*
            if(typeof scriptParameters.passwordIndex != 'undefined') {
              var PasswordIndex = parseInt(scriptParameters.passwordIndex,10);
              if(PasswordIndex &lt; 1 &amp;&amp; PasswordIndex &gt; 4)
                throw "SecurityMode: Key index must be between 1 and 4";
              cpeParameters.passwordIndex.value = scriptParameters.passwordIndex;
              cpeParameters.passwordIndex.updated = true;
            } else {
              throw "SecurityMode(a):Key index must be between 1 and 4";
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
            */

            if(value == "WEP-Shared") {
              cpeParameters.BasicAuthenticationMode.value = "SharedAuthentication";
              cpeParameters.BasicAuthenticationMode.updated = true;
              if (typeof scriptParameters.password != 'undefined' &amp;&amp; scriptParameters.password !== null) {
                if(scriptParameters.password.length !== 0 &amp;&amp; scriptParameters.password.length != 10)
                  throw "Password length invalid. Must be 10 ASCII characters";
                cpeParameters.passwordIndex.value = PasswordIndex;
                cpeParameters.passwordIndex.updated = true;
                cpeParameters.password1.value = scriptParameters.password;
                cpeParameters.password1.updated = true;
              }
              else {
                if(typeof scriptParameters.passwordIndex != 'undefined') {
                  PasswordIndex = parseInt(scriptParameters.passwordIndex,10);
                  if(PasswordIndex &lt; 1 &amp;&amp; PasswordIndex &gt; 4)
                    throw "SecurityMode: Key index must be between 1 and 4";
                  cpeParameters.passwordIndex.value = scriptParameters.passwordIndex;
                  cpeParameters.passwordIndex.updated = true;
        
                  if (typeof scriptParameters.password1 != 'undefined' &amp;&amp; scriptParameters.password1 !== null) {
                    if(scriptParameters.password1.length !== 0 &amp;&amp; scriptParameters.password1.length != 10) 
                      throw "Password length invalid. Must be 10 ASCII characters";
                    cpeParameters.password1.value = scriptParameters.password1;
                    cpeParameters.password1.updated = true;
                  }
                } 
              }
            } else {
              cpeParameters.BasicAuthenticationMode.value = "None";
              cpeParameters.BasicAuthenticationMode.updated = true;
              if (typeof scriptParameters.password != 'undefined' &amp;&amp; scriptParameters.password !== null) {
                if(scriptParameters.password.length !== 0 &amp;&amp; scriptParameters.password.length != 13)
                  throw "Password length invalid. Must be 13 ASCII characters";
                cpeParameters.passwordIndex.value = PasswordIndex;
                cpeParameters.passwordIndex.updated = true;
                cpeParameters.password1.value = scriptParameters.password;
                cpeParameters.password1.updated = true;
              }
              else {
                if(typeof scriptParameters.passwordIndex != 'undefined') {
                  PasswordIndex = parseInt(scriptParameters.passwordIndex,10);
                  if(PasswordIndex &lt; 1 &amp;&amp; PasswordIndex &gt; 4)
                    throw "SecurityMode: Key index must be between 1 and 4";
                  cpeParameters.passwordIndex.value = scriptParameters.passwordIndex;
                  cpeParameters.passwordIndex.updated = true;
        
                  if (typeof scriptParameters.password1 != 'undefined' &amp;&amp; scriptParameters.password1 !== null) {
                    if(scriptParameters.password1.length !== 0 &amp;&amp; scriptParameters.password1.length != 13)
                      throw "Password length invalid. Must be 13 ASCII characters";
                    cpeParameters.password1.value = scriptParameters.password1;
                    cpeParameters.password1.updated = true;
                  }
                } 
              }
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
            
            if (typeof scriptParameters.password != 'undefined' &amp;&amp; scriptParameters.password !== null) {
              if(scriptParameters.password.length &lt; 8)
                throw "Password length invalid. Must be 8-63 ASCII characters";
              cpeParameters.password.value = scriptParameters.password;
              cpeParameters.password.updated = true;
            }
                        
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

            if (typeof scriptParameters.password != 'undefined' &amp;&amp; scriptParameters.password !== null) {
              if(scriptParameters.password.length &lt; 8)
                throw "Password length invalid. Must be 8-63 ASCII characters";
              cpeParameters.password.value = scriptParameters.password;
              cpeParameters.password.updated = true;
            }
           
          }
          break;
     default : 
          break;
    }
  }
  return cpeParameters;
}


response;</javaScriptCode>
        </scriptDefinition>
    </deviceServiceConfigurations>
    <deviceServiceConfigurations name="Device Log">
        <scriptDefinition name="ZTE_H196A_V9-LAB: Device Log" purpose="Device service configuration" tags="null" scriptParameters="[]">
            <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var deviceId = scriptParameters.deviceId;
var response = dsc.getDeviceParameterLogs(deviceId);

response;
</javaScriptCode>
        </scriptDefinition>
    </deviceServiceConfigurations>
    <deviceServiceConfigurations name="WiFi 8">
        <scriptDefinition name="ZTE_H196A_V9-LAB: WiFi 8" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="WiFi 6">
        <scriptDefinition name="ZTE_H196A_V9-LAB: WiFi 6" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="TR-69 Config">
        <scriptDefinition name="ZTE_H196A_V9-LAB: TR-69 Config" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="DHCP">
        <scriptDefinition name="ZTE_H196A_V9-LAB: DHCP" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="WiFi 4">
        <scriptDefinition name="ZTE_H196A_V9-LAB: WiFi 4" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="WiFi 2">
        <scriptDefinition name="ZTE_H196A_V9-LAB: WiFi 2" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="WiFi 7">
        <scriptDefinition name="ZTE_H196A_V9-LAB: WiFi 7" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="WiFi 3">
        <scriptDefinition name="ZTE_H196A_V9-LAB: WiFi 3" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <dataComposers name="Bytes Received">
        <scriptDefinition name="ZTE_H196A_V9-LAB: Bytes Received" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <dataComposers name="Bytes Sent">
        <scriptDefinition name="ZTE_H196A_V9-LAB: Bytes Sent" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <dashboardPanelScripts>
        <dashboardPanelScript name="##dashboard.connected_devices_topology.name##" scriptType="DASHBOARD_SCRIPT">
            <scriptDefinition name="ZTE_H196A_V9-LAB:##dashboard.connected_devices_topology.name##" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
            <scriptDefinition name="ZTE_H196A_V9-LAB:##dashboard.tr069_config.name##" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
        <dashboardPanelScript name="##dashboard.device_info.name##" scriptType="DASHBOARD_SCRIPT">
            <scriptDefinition name="ZTE_H196A_V9-LAB:##dashboard.device_info.name##" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    </dashboardPanelScripts>
    <scriptSupportedLanguages code="fr_ca">
        <keywords name="wifi.transmit_power" description="Puissance de transmission"/>
        <keywords name="wifi.frequency" description="La fréquence"/>
        <keywords name="wifi.wifi_enable" description="Activée"/>
        <keywords name="wifi.ssid" description="SSID"/>
        <keywords name="wifi.channel_width" description="Largeur du canal"/>
        <keywords name="wifi.password_index" description="Indice de mots de passe"/>
        <keywords name="wifi.broadcast_ssid" description="SSID de diffusion"/>
        <keywords name="wifi.channel" description="Canal WiFi"/>
        <keywords name="wifi.password" description="Mot de passe"/>
        <keywords name="wifi.security_mode" description="Mode de sécurité"/>
    </scriptSupportedLanguages>
    <scriptSupportedLanguages code="en">
        <keywords name="wifi.transmit_power" description="Transmit power"/>
        <keywords name="wifi.frequency" description="Frequency"/>
        <keywords name="wifi.wifi_enable" description="Enabled"/>
        <keywords name="wifi.ssid" description="SSID"/>
        <keywords name="wifi.channel_width" description="Channel width"/>
        <keywords name="wifi.password_index" description="Password index"/>
        <keywords name="wifi.broadcast_ssid" description="Broadcast SSID"/>
        <keywords name="wifi.channel" description="Channel"/>
        <keywords name="wifi.password" description="Password"/>
        <keywords name="wifi.security_mode" description="Security Mode"/>
    </scriptSupportedLanguages>
    <scriptSupportedLanguages code="fr">
        <keywords name="wifi.transmit_power" description="Puissance de transmission"/>
        <keywords name="wifi.frequency" description="La fréquence"/>
        <keywords name="wifi.wifi_enable" description="Activée"/>
        <keywords name="wifi.ssid" description="SSID"/>
        <keywords name="wifi.channel_width" description="Largeur du canal"/>
        <keywords name="wifi.password_index" description="Indice de mots de passe"/>
        <keywords name="wifi.broadcast_ssid" description="SSID de diffusion"/>
        <keywords name="wifi.channel" description="Canal WiFi"/>
        <keywords name="wifi.password" description="Mot de passe"/>
        <keywords name="wifi.security_mode" description="Mode de sécurité"/>
    </scriptSupportedLanguages>
    <scriptSupportedLanguages code="es">
        <keywords name="wifi.transmit_power" description="Potencia de Transmissión"/>
        <keywords name="wifi.frequency" description="Frecuencia"/>
        <keywords name="wifi.wifi_enable" description="Activo"/>
        <keywords name="wifi.ssid" description="SSID"/>
        <keywords name="wifi.channel_width" description="Ancho de canal"/>
        <keywords name="wifi.password_index" description="índice de contraseña"/>
        <keywords name="wifi.broadcast_ssid" description="Propagación de SSID"/>
        <keywords name="wifi.channel" description="Canal"/>
        <keywords name="wifi.password" description="Contraseña"/>
        <keywords name="wifi.security_mode" description="Modo de seguridad"/>
    </scriptSupportedLanguages>
    <scriptSupportedLanguages code="zh">
        <keywords name="wifi.transmit_power" description="发射功率"/>
        <keywords name="wifi.frequency" description="频率"/>
        <keywords name="wifi.wifi_enable" description="开启"/>
        <keywords name="wifi.ssid" description="SSID"/>
        <keywords name="wifi.channel_width" description="信道带宽"/>
        <keywords name="wifi.password_index" description="密码索引"/>
        <keywords name="wifi.broadcast_ssid" description="广播 SSID"/>
        <keywords name="wifi.channel" description="信道"/>
        <keywords name="wifi.password" description="密码"/>
        <keywords name="wifi.security_mode" description="安全模式"/>
    </scriptSupportedLanguages>
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
        <widgets name="WiFi 8" type="SERVICE_CONFIGURATION" description="Wireless Network" stale="true">
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 8</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="WiFi 3" type="SERVICE_CONFIGURATION" description="Wireless Network" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">wifi-signal</value>
                </entry>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">19</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 3</value>
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
        <widgets name="WiFi 4" type="SERVICE_CONFIGURATION" description="Wireless Network" stale="true">
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 4</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="WiFi 7" type="SERVICE_CONFIGURATION" description="Wireless Network" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">wifi-signal</value>
                </entry>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 7</value>
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
        <widgets name="Device Log" type="SERVICE_CONFIGURATION" description="Device Log" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">file</value>
                </entry>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">28</value>
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
        <widgets name="WiFi 1" type="SERVICE_CONFIGURATION" description="Wireless Network" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">wifi-signal</value>
                </entry>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">22</value>
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
        <widgets name="Diagnostics" type="DIAGNOSTICS" description="Device Diagnostics" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">stethoscope</value>
                </entry>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">24</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
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
        <widgets name="DHCP" type="SERVICE_CONFIGURATION" description="Device DHCP" stale="true">
            <configuration>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">23</value>
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
        <widgets name="WiFi 6" type="SERVICE_CONFIGURATION" description="Wireless Network" stale="true">
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 6</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">25</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">26</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">27</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">21</value>
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
        <widgets name="WiFi 5" type="SERVICE_CONFIGURATION" description="Wireless Network" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">wifi-signal</value>
                </entry>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">20</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 5</value>
                </entry>
            </configuration>
        </widgets>
        <allowAllGroups>TRUE</allowAllGroups>
        <config/>
    </dashboards>
    <dashboardPanels>
        <dashboardPanel name="##dashboard.failed_operations.name##" panelType="PANEL_STATUS_OPERATIONS_FAILED">
            <configuration>{"links":{"#panelStatusOperationsFailed":{"url":"#devices/{deviceId}/failed-operations"}},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"rules":{"type":"numeric","threshold":"NONE"},"unit":null}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.tr069_config.name##" panelType="PANEL_DASHBOARD_TR069_CONFIG">
            <configuration>{"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"##dashboard.tr069_config.name##","sourceIdSet":[]},"buttons":{"handlers":[{"text":"Save","handler":"saveServiceConfigParameters","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"POST"},"visible":true,"tab":null},{"text":"Cancel","handler":"cancel","endpoint":{"url":"/deviceoperations/cancellation","verb":"POST"},"visible":false,"tab":null},{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"readOnly":false}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.up_time.name##" panelType="PANEL_STATUS_UPTIME">
            <configuration>{"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.DeviceInfo.UpTime","sourceIdSet":[]},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"duration":{"enable":true,"unit":"seconds"}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.traceroute.name##" panelType="PANEL_DASHBOARD_TRACEROUTE">
            <configuration>{"buttons":{"handlers":[{"text":"Run","handler":"runDiagnostics","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"POST"},"visible":true,"tab":null},{"text":"Cancel","handler":"cancelDiagnostics","endpoint":{"url":"/deviceoperations/cancellation","verb":"POST"},"visible":false,"tab":null}]},"diagnosticsConfig":[{"id":"TraceRoute Diagnostics","subType":"TRACEROUTE","diagnosticParameters":[{"name":"InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount","value":null},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.Host","value":null},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.Timeout","value":null},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries","value":null},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.Interface","value":null},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize","value":null},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.DSCP","value":null}]}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.session_info.name##" panelType="PANEL_DASHBOARD_SESSION_INFO">
            <configuration>{"buttons":{"handlers":[{"text":"Initiate Session","handler":"initiateSession","endpoint":{"url":"/devices/{deviceId}/connectionrequest?async=true","verb":"POST"},"visible":true,"tab":null}]},"websockets":{"ws":"/devices/{deviceId}?X-Atmosphere-tracking-id=0&amp;X-Cache-Date=0&amp;Content-Type=application/json&amp;X-atmo-protocol=true","handlers":[{"type":"TR69_INFORM_EVENT"},{"type":"TR69_SESSION_EVENT"},{"type":"TR69_CONNECTION_REQUEST_EVENT"}]},"readOnly":false}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.device_actions.name##" panelType="PANEL_DEVICE_OPERATIONS_ACTIONS">
            <configuration>{"actionsConfig":[],"moreButton":{"handlers":[{"text":"##dashboard.more_device_actions##","handler":"showMoreActions","visible":true}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.admin_actions.name##" panelType="PANEL_DEVICE_OPERATIONS_ADMIN">
            <configuration>{"actionsConfig":[{"id":"ManageOperation","text":"Manage Operations","url":"#devices/{deviceId}/active-operations","order":1,"visible":true},{"id":"ObjectStructParameter","text":"Manage Object Structure &amp; Parameters","url":"#devices/{deviceId}/parameters","order":2,"visible":true},{"id":"ManageGroupings","text":"Manage Groupings","url":"#devices/{deviceId}/device-groups","order":3,"visible":true},{"id":"ViewDeviceInfo","text":"View Device Information","url":"#devices/{deviceId}/device","order":4,"visible":true},{"id":"DeviceWorkbench","text":"Device Workbench","url":"#devices/{deviceId}/workbench","order":5,"visible":true},{"id":"ComplianceTestSuite","text":"Run Compliance Test Suite","url":"#devices/{deviceId}/execute-device-compliance-suite","order":6,"visible":true},{"id":"PerformActions","text":"Perform Actions","url":"#devices/{deviceId}/devicemodel/{deviceModelId}/device_actions","order":7,"visible":true},{"id":"PerformDiagnostics","text":"Perform Diagnostics","url":"#devices/{deviceId}/devicemodel/{deviceModelId}/diagnostics","order":8,"visible":true}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.active_operations.name##" panelType="PANEL_STATUS_OPERATIONS_ACTIVE">
            <configuration>{"links":{"#panelStatusOperationsActive":{"url":"#devices/{deviceId}/active-operations"}},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"rules":{"type":"numeric","threshold":"NONE"},"unit":null}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Broadband Speed Test" panelType="PANEL_DASHBOARD_BROADBAND_SPEED">
            <configuration>{"diagnosticsConfig":[{"id":"Download Diagnostics","subType":"DOWNLOADSPEED","diagnosticParameters":[{"name":"InternetGatewayDevice.DownloadDiagnostics.DownloadURL","value":"http://35.215.210.14:9090/download.bin"},{"name":"InternetGatewayDevice.DownloadDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.DownloadDiagnostics.DSCP","value":""},{"name":"InternetGatewayDevice.DownloadDiagnostics.EthernetPriority","value":""}]},{"id":"Upload Diagnostics","subType":"UPLOADSPEED","diagnosticParameters":[{"name":"InternetGatewayDevice.UploadDiagnostics.EthernetPriority","value":""},{"name":"InternetGatewayDevice.UploadDiagnostics.UploadURL","value":"http://35.215.210.14:9090/upload.bin"},{"name":"InternetGatewayDevice.UploadDiagnostics.DSCP","value":""},{"name":"InternetGatewayDevice.UploadDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.UploadDiagnostics.TestFileLength","value":"1000"}]}],"tabName":"98fb32c6-5c3a-ae4a-3999-3a52118865a1","downloadEnabled":true,"uploadEnabled":true,"InternetGatewayDevice.DownloadDiagnostics.DownloadURL":"http://35.215.210.14:9090/download.bin","InternetGatewayDevice.DownloadDiagnostics.Interface":"","InternetGatewayDevice.DownloadDiagnostics.DSCP":"","InternetGatewayDevice.DownloadDiagnostics.EthernetPriority":"","InternetGatewayDevice.UploadDiagnostics.EthernetPriority":"","InternetGatewayDevice.UploadDiagnostics.UploadURL":"http://35.215.210.14:9090/upload.bin","InternetGatewayDevice.UploadDiagnostics.DSCP":"","InternetGatewayDevice.UploadDiagnostics.Interface":"","InternetGatewayDevice.UploadDiagnostics.TestFileLength":"1000"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.device_info.name##" panelType="PANEL_DASHBOARD_DEVICE_INFO">
            <configuration>{"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"##dashboard.device_info.name##","sourceIdSet":[]},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"panelType":"PANEL_STATUS_ONLINE"}}]},"buttons":{"handlers":[{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"readOnly":true}</configuration>
        </dashboardPanel>
        <dashboardPanel name="IP Ping Test" panelType="PANEL_DASHBOARD_IPPING">
            <configuration>{"diagnosticsConfig":[{"id":"IP Ping Diagnostics","subType":"IPPING","diagnosticParameters":[{"name":"InternetGatewayDevice.IPPingDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.IPPingDiagnostics.Host","value":"8.8.8.8"},{"name":"InternetGatewayDevice.IPPingDiagnostics.DSCP","value":""},{"name":"InternetGatewayDevice.IPPingDiagnostics.DataBlockSize","value":""},{"name":"InternetGatewayDevice.IPPingDiagnostics.Timeout","value":""},{"name":"InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions","value":""}]}],"tabName":"5c987c0f-f453-1f54-be91-71c4bb6aed6c","InternetGatewayDevice.IPPingDiagnostics.Interface":"","InternetGatewayDevice.IPPingDiagnostics.Host":"8.8.8.8","InternetGatewayDevice.IPPingDiagnostics.DSCP":"","InternetGatewayDevice.IPPingDiagnostics.DataBlockSize":"","InternetGatewayDevice.IPPingDiagnostics.Timeout":"","InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions":""}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.sync_status.name##" panelType="PANEL_STATUS_SYNC">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Utilização Canal 2.4Ghz" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"a839facf-9c47-578c-3c84-70b47c95c2e3","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/c44a9eb0-ba99-11ec-96e0-c516b8f93291?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:'0.1',filter:(language:kuery,query:''),formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'',line_width:1,metrics:!((id:'61ca57f2-469d-11e7-af02-69e470af7417',type:count)),point_size:1,separate_axis:0,split_color_mode:kibana,split_filters:!((color:%2368BC00,filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%201'),id:c0235550-902a-11ec-8823-65b10961c04e,label:'Canal%201'),(color:'rgba(84,179,153,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%202'),id:c94521e0-902a-11ec-8823-65b10961c04e,label:'Canal%202'),(color:'rgba(211,96,134,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%203'),id:d3408590-902a-11ec-8823-65b10961c04e,label:'Canal%203'),(color:'rgba(145,112,184,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%204'),id:d7d269c0-902a-11ec-8823-65b10961c04e,label:'Canal%204'),(color:'rgba(202,142,174,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%205'),id:dd5341d0-902a-11ec-8823-65b10961c04e,label:'Canal%205'),(color:'rgba(214,191,87,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%206'),id:e0a727c0-902a-11ec-8823-65b10961c04e,label:'Canal%206'),(color:'rgba(185,168,136,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%207'),id:e76b5540-902a-11ec-8823-65b10961c04e,label:'Canal%207'),(color:'rgba(218,139,69,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%208'),id:ea256c30-902a-11ec-8823-65b10961c04e,label:'Canal%208'),(color:'rgba(170,101,86,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%209'),id:eda32140-902a-11ec-8823-65b10961c04e,label:'Canal%209'),(color:'rgba(231,102,76,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%2010'),id:f106bea0-902a-11ec-8823-65b10961c04e,label:'Canal%2010'),(color:'rgba(22,0,188,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel:%2011'),id:f3c1bff0-902a-11ec-8823-65b10961c04e,label:'Canal%2011')),split_mode:filters,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Channel%202.4%20Geral%20-%20Per%20Device',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.connected_devices_topology.name##" panelType="PANEL_DASHBOARD_CONNECTED_DEVICES">
            <configuration>{"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"##dashboard.connected_devices_topology.name##","sourceIdSet":[]},"buttons":{"handlers":[{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"readOnly":false}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.connected_devices.name##" panelType="PANEL_STATUS_CONNECTED">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"rules":{"type":"numeric","threshold":"NONE"}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="WiFi 2.4Ghz" panelType="PANEL_DASHBOARD_SERVICE_CONFIG">
            <configuration>{"readOnly":false,"tabName":"a839facf-9c47-578c-3c84-70b47c95c2e3","dataSource":{"type":"SERVICE_CONFIGURATION_SCRIPT","sourceId":"WiFi 1","sourceIdSet":[]},"diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_SERVICE_CONFIG","dataType":"SERVICE_CONFIGURATION_SCRIPT","dataSourceServiceConfig":"6c2a2483-5cfd-58de-77ec-609e4f51e947"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Utilização Canal 5Ghz" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"a839facf-9c47-578c-3c84-70b47c95c2e3","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/2872d820-bb22-11ec-96e0-c516b8f93291?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:'0.1',filter:(language:kuery,query:''),formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'',line_width:1,metrics:!((id:'61ca57f2-469d-11e7-af02-69e470af7417',type:count)),point_size:1,separate_axis:0,split_color_mode:kibana,split_filters:!((color:%2368BC00,filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2036'),id:c0235550-902a-11ec-8823-65b10961c04e,label:'Canal%2036'),(color:'rgba(84,179,153,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel:%2040'),id:c94521e0-902a-11ec-8823-65b10961c04e,label:'Canal%2040'),(color:'rgba(211,96,134,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2044'),id:d3408590-902a-11ec-8823-65b10961c04e,label:'Channel%2044'),(color:'rgba(145,112,184,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2048'),id:d7d269c0-902a-11ec-8823-65b10961c04e,label:'Channel%2048'),(color:'rgba(202,142,174,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2052'),id:dd5341d0-902a-11ec-8823-65b10961c04e,label:'Channel%2052'),(color:'rgba(214,191,87,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2056'),id:e0a727c0-902a-11ec-8823-65b10961c04e,label:'Channel%2056'),(color:'rgba(185,168,136,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2060'),id:e76b5540-902a-11ec-8823-65b10961c04e,label:'Channel%2060'),(color:'rgba(218,139,69,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2064'),id:ea256c30-902a-11ec-8823-65b10961c04e,label:'Channel%2064'),(color:'rgba(170,101,86,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20100'),id:eda32140-902a-11ec-8823-65b10961c04e,label:'Channel%20100'),(color:'rgba(231,102,76,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20104'),id:f106bea0-902a-11ec-8823-65b10961c04e,label:'Channel%20104'),(color:'rgba(22,0,188,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20108'),id:f3c1bff0-902a-11ec-8823-65b10961c04e,label:'Channel%20108'),(color:'rgba(231,240,129,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20112'),id:cce01c50-90c1-11ec-8419-030540e36e5c,label:'Channel%20112'),(color:'rgba(115,232,113,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20116'),id:d16667c0-90c1-11ec-8419-030540e36e5c,label:'Channel%20116'),(color:'rgba(130,80,107,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20120'),id:d4d3c920-90c1-11ec-8419-030540e36e5c,label:'Channel%20120'),(color:'rgba(247,112,112,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel:%20124'),id:dd5c62f0-90c1-11ec-8419-030540e36e5c,label:'Channel%20124'),(color:'rgba(1,120,66,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20128'),id:e29387d0-90c1-11ec-8419-030540e36e5c,label:'Channel%20128'),(color:'rgba(235,198,97,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20132'),id:e7a6f810-90c1-11ec-8419-030540e36e5c,label:'Channel%20132'),(color:'rgba(205,98,139,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20136'),id:ed97f710-90c1-11ec-8419-030540e36e5c,label:'Channel%20136'),(color:'rgba(50,62,122,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20140'),id:f3d2a940-90c1-11ec-8419-030540e36e5c,label:'Channel%20140'),(color:'rgba(41,105,128,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20144'),id:f5baa320-90c1-11ec-8419-030540e36e5c,label:'Channel%20144'),(color:'rgba(38,67,83,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20149'),id:f9f3e000-90c1-11ec-8419-030540e36e5c,label:'Channel%20149'),(color:'rgba(96,125,61,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20153'),id:'518470a0-b4e4-11ec-8956-e556ebb5a566',label:'Channel%20153'),(color:'rgba(246,151,182,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20157'),id:'64c814a0-b4e4-11ec-8956-e556ebb5a566',label:'Channel%20157'),(color:'rgba(236,205,177,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel:%20161'),id:'7047f570-b4e4-11ec-8956-e556ebb5a566',label:'Channel%20161')),split_mode:filters,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Channel%205Ghz%20Geral%20-%20Per%20Device',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.online.name##" panelType="PANEL_STATUS_ONLINE">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.broadband_speed_hist.name##" panelType="PANEL_DASHBOARD_BROADBAND_HISTORICAL">
            <configuration>{"buttons":{"handlers":[{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"tableConfig":{"searchName":"PANEL_DASHBOARD_BROADBAND_HISTORICAL","title":"Historic Broadband Speed Test Results","searchParams":{"tableName":"DIAGNOSTIC_RESULT_SUMMARY","url":"/devices/{deviceId}/diagnostics/speedtest","q":"PINGTESTDATE is null","pageSize":20,"orderBy":"LASTMODIFIED","ascending":false},"columns":[{"name":"time","field":"lastModified","label":"Time","align":"left","dataType":"DATETIME","fieldFormat":"hh:mma, dd MMM yyyy"},{"name":"dload","field":"downloadSpeed","label":"Download Speed (Mbps)","align":"center","dataType":"MBYTES","fieldFormat":"%.1f"},{"name":"uload","field":"uploadSpeed","label":"Upload Speed (Mbps)","align":"center","dataType":"MBYTES","fieldFormat":"%.1f"}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="WiFi 5Ghz" panelType="PANEL_DASHBOARD_SERVICE_CONFIG">
            <configuration>{"readOnly":false,"tabName":"a839facf-9c47-578c-3c84-70b47c95c2e3","dataSource":{"type":"SERVICE_CONFIGURATION_SCRIPT","sourceId":"WiFi 5","sourceIdSet":[]},"diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_SERVICE_CONFIG","dataType":"SERVICE_CONFIGURATION_SCRIPT","dataSourceServiceConfig":"4ce097b3-a962-310a-e09c-da457efa5340"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.common_issues.name##" panelType="PANEL_DEVICE_OPERATIONS_ISSUES">
            <configuration>{"actionsConfig":[{"order":0,"include":true,"text":"Incognito Support","url":"https://support.incognito.com/"}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.last_seen.name##" panelType="PANEL_STATUS_LASTSEEN">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"duration":{"enable":false,"unit":null}}</configuration>
        </dashboardPanel>
    </dashboardPanels>
    <dashboardLayout>{"version":"1.2","children":[{"type":"COLUMN_LEFT","order":0,"hasPanelChildren":false,"children":[{"name":"##dashboard.layout.region.device_ident##","type":"REGION_DEVICE_IDENTIFIER","order":0,"hasPanelChildren":false,"children":[{"name":"PANEL_COMMON_DEVICE_IDENTIFIER","type":"PANEL_COMMON_DEVICE_IDENTIFIER","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.customer_ident##","type":"REGION_CUSTOMER_IDENTIIFIER","order":1,"hasPanelChildren":true,"children":[{"name":"PANEL_COMMON_CUSTOMER_IDENTIFIER","type":"PANEL_COMMON_CUSTOMER_IDENTIFIER","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.images##","type":"REGION_DEVICE_IMAGES","order":2,"hasPanelChildren":true,"children":[{"name":"PANEL_COMMON_DEVICE_IMAGES","type":"PANEL_COMMON_DEVICE_IMAGES","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.operations##","type":"REGION_DEVICE_OPERATIONS","order":3,"hasPanelChildren":true,"children":[{"name":"##dashboard.device_actions.name##","type":"PANEL_DEVICE_OPERATIONS_ACTIONS","order":0,"hasPanelChildren":false},{"name":"##dashboard.common_issues.name##","type":"PANEL_DEVICE_OPERATIONS_ISSUES","order":1,"hasPanelChildren":false},{"name":"##dashboard.admin_actions.name##","type":"PANEL_DEVICE_OPERATIONS_ADMIN","order":2,"hasPanelChildren":false}]}]},{"type":"COLUMN_RIGHT","order":1,"hasPanelChildren":false,"children":[{"name":"##dashboard.layout.region.status##","type":"REGION_STATUS","order":0,"hasPanelChildren":true,"children":[{"name":"##dashboard.online.name##","type":"PANEL_STATUS_ONLINE","order":0,"hasPanelChildren":false},{"name":"##dashboard.last_seen.name##","type":"PANEL_STATUS_LASTSEEN","order":1,"hasPanelChildren":false},{"name":"##dashboard.sync_status.name##","type":"PANEL_STATUS_SYNC","order":2,"hasPanelChildren":false},{"name":"##dashboard.connected_devices.name##","type":"PANEL_STATUS_CONNECTED","order":3,"hasPanelChildren":false},{"name":"##dashboard.active_operations.name##","type":"PANEL_STATUS_OPERATIONS_ACTIVE","order":4,"hasPanelChildren":false},{"name":"##dashboard.failed_operations.name##","type":"PANEL_STATUS_OPERATIONS_FAILED","order":5,"hasPanelChildren":false},{"name":"##dashboard.up_time.name##","type":"PANEL_STATUS_UPTIME","order":6,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.csr_call_log##","type":"REGION_CSR_CALL_INFO","order":1,"hasPanelChildren":true,"children":[{"name":"##dashboard.csr_call_info.name##","type":"PANEL_COMMON_CSR_CALL_INFO","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.dashboards##","type":"REGION_DASHBOARDS","order":2,"hasPanelChildren":false,"children":[{"name":"##dashboard.tab.overview##","type":"TAB_DASHBOARD","order":0,"hasPanelChildren":true,"visible":true,"children":[{"name":"##dashboard.device_info.name##","type":"PANEL_DASHBOARD_DEVICE_INFO","order":0,"hasPanelChildren":false,"size":{"h":1,"v":1}},{"name":"Broadband Speed Test","type":"PANEL_DASHBOARD_BROADBAND_SPEED","order":1,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"##dashboard.broadband_speed_hist.name##","type":"PANEL_DASHBOARD_BROADBAND_HISTORICAL","order":2,"hasPanelChildren":false,"size":{"h":1,"v":1}},{"name":"##dashboard.session_info.name##","type":"PANEL_DASHBOARD_SESSION_INFO","order":3,"hasPanelChildren":false,"size":{"h":1,"v":1}}]},{"name":"##dashboard.tab.topology##","type":"TAB_DASHBOARD","order":1,"hasPanelChildren":true,"visible":false,"children":[{"name":"##dashboard.connected_devices_topology.name##","type":"PANEL_DASHBOARD_CONNECTED_DEVICES","order":0,"hasPanelChildren":false,"size":{"h":2,"v":1}}]},{"name":"##dashboard.tab.diagnostics##","type":"TAB_DASHBOARD","order":2,"hasPanelChildren":true,"visible":false,"children":[{"name":"##dashboard.tr069_config.name##","type":"PANEL_DASHBOARD_TR069_CONFIG","order":0,"hasPanelChildren":false,"size":{"h":1,"v":1}},{"name":"IP Ping Test","type":"PANEL_DASHBOARD_IPPING","order":1,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"##dashboard.traceroute.name##","type":"PANEL_DASHBOARD_TRACEROUTE","order":2,"hasPanelChildren":false,"size":{"h":1,"v":1}}]},{"name":"WiFi","type":"TAB_DASHBOARD","order":3,"hasPanelChildren":true,"visible":true,"children":[{"name":"WiFi 2.4Ghz","type":"PANEL_DASHBOARD_SERVICE_CONFIG","order":0,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"WiFi 5Ghz","type":"PANEL_DASHBOARD_SERVICE_CONFIG","order":1,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"Utilização Canal 2.4Ghz","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":2,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Utilização Canal 5Ghz","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":3,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":2,"v":1}}]}]}]}]}</dashboardLayout>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.PacketsRX" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.PacketsRX" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.PacketsRX" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.MaximumActiveConnections" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.MaximumActiveConnections" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.Queue.{i}.ShapingBurstSize" elementDefinition="InternetGatewayDevice.QueueManagement.Queue.{i}.ShapingBurstSize" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.EOMTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.EOMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.MaxClassificationEntries" elementDefinition="InternetGatewayDevice.QueueManagement.MaxClassificationEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.DuplexMode" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.DuplexMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.BOMTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.BOMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.EnablePerConnectionResults" elementDefinition="InternetGatewayDevice.UploadDiagnostics.EnablePerConnectionResults" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.EnablePerConnectionResults" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.StaticType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.StaticType" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.StaticType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MACAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MACAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.X_ZTE-COM_PollInterval" elementDefinition="InternetGatewayDevice.Time.X_ZTE-COM_PollInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Time.X_ZTE-COM_PollInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.AL_MAC" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.AL_MAC" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.AL_MAC" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.GatewayInfo.SerialNumber" elementDefinition="InternetGatewayDevice.GatewayInfo.SerialNumber" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.GatewayInfo.SerialNumber" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.UploadDiagnostics.DSCP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.X_ZTE-COM_DSCP" elementDefinition="InternetGatewayDevice.Time.X_ZTE-COM_DSCP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Time.X_ZTE-COM_DSCP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.DeviceLog" elementDefinition="InternetGatewayDevice.DeviceInfo.DeviceLog" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MACAddressControlEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MACAddressControlEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.Queue.{i}.QueueWeight" elementDefinition="InternetGatewayDevice.QueueManagement.Queue.{i}.QueueWeight" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.Enable" elementDefinition="InternetGatewayDevice.UDPEchoConfig.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.UploadDiagnosticMaxConnections" elementDefinition="InternetGatewayDevice.UploadDiagnostics.UploadDiagnosticMaxConnections" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.UploadDiagnosticMaxConnections" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNUsername" elementDefinition="InternetGatewayDevice.ManagementServer.STUNUsername" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.Layer2Interface" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.Layer2Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.TotalSTANumberOfEntries" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.TotalSTANumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.TotalSTANumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.EnablePerConnectionResults" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.EnablePerConnectionResults" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.EnablePerConnectionResults" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.Interface" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DNSServers" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DNSServers" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.AdditionalHardwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.AdditionalHardwareVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UploadTransports" elementDefinition="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UploadTransports" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.Username" elementDefinition="InternetGatewayDevice.ManagementServer.Username" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6DefaultConnectionService" elementDefinition="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6DefaultConnectionService" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6DefaultConnectionService" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.PeriodicInformInterval" elementDefinition="InternetGatewayDevice.ManagementServer.PeriodicInformInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDeviceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDeviceNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.ClientID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.ClientID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.PrefixDelegationType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.PrefixDelegationType" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.PrefixDelegationType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_Mirror.Enable" elementDefinition="InternetGatewayDevice.X_ZTE-COM_Mirror.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_Mirror.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.NextHop" elementDefinition="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.NextHop" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.NextHop" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WIFI.Radio.{i}.DiagnosticsState" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WIFI.Radio.{i}.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WIFI.Radio.{i}.DiagnosticsState" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.STA.{i}.SignalStrength" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.STA.{i}.SignalStrength" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.STA.{i}.SignalStrength" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.TimeFirstPacketReceived" elementDefinition="InternetGatewayDevice.UDPEchoConfig.TimeFirstPacketReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSentUnderFullLoading" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSentUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSentUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.DownloadTransports" elementDefinition="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.DownloadTransports" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Version" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Version" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Version" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Alias" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Alias" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Alias" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.AdditionalSoftwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.AdditionalSoftwareVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKeyIndex" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKeyIndex" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.ClassificationNumberOfEntries" elementDefinition="InternetGatewayDevice.QueueManagement.ClassificationNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.SuccessCount" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.SuccessCount" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.DataBlockSize" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.DataBlockSize" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddress" elementDefinition="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.STA.{i}.AccessType" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.STA.{i}.AccessType" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.STA.{i}.AccessType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnReqAllowedJabberIDs" elementDefinition="InternetGatewayDevice.ManagementServer.ConnReqAllowedJabberIDs" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.ConnReqAllowedJabberIDs" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.HardwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.HardwareVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.User.{i}.Password" elementDefinition="InternetGatewayDevice.User.{i}.Password" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.User.{i}.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.MaximumResponseTime" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.MaximumResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DNS.X_ZTE-COM_DomainName" elementDefinition="InternetGatewayDevice.DNS.X_ZTE-COM_DomainName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DNS.X_ZTE-COM_DomainName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.PPTPEnable" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.PPTPEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.PPTPEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.MaxRtrAdvInterval" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.MaxRtrAdvInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.MaxRtrAdvInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.H323Enable" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.H323Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.H323Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.TFTPEnable" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.TFTPEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.TFTPEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.LocalTimeZoneName" elementDefinition="InternetGatewayDevice.Time.LocalTimeZoneName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.DestIPPrefix" elementDefinition="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.DestIPPrefix" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.DestIPPrefix" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_BandWidth" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_BandWidth" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_BandWidth" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.IPSECEnable" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.IPSECEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.IPSECEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.SoftwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.SoftwareVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_Mirror.SrcInterface" elementDefinition="InternetGatewayDevice.X_ZTE-COM_Mirror.SrcInterface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_Mirror.SrcInterface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.OperationalDataTransmitRates" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.OperationalDataTransmitRates" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_DDNS.Enable" elementDefinition="InternetGatewayDevice.X_ZTE-COM_DDNS.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_DDNS.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceived" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DomainName" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DomainName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Remotelog.LogServer" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Remotelog.LogServer" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Remotelog.LogServer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.Status" elementDefinition="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.Status" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.Status" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.ValidLifetime" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.ValidLifetime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.ValidLifetime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.STA.{i}.MAC" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.STA.{i}.MAC" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.STA.{i}.MAC" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PossibleChannels" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PossibleChannels" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_UPnP.Interface" elementDefinition="InternetGatewayDevice.X_ZTE-COM_UPnP.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_UPnP.Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_MLD.SnoopingEnable" elementDefinition="InternetGatewayDevice.X_ZTE-COM_MLD.SnoopingEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_MLD.SnoopingEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.SourceIPAddress" elementDefinition="InternetGatewayDevice.UDPEchoConfig.SourceIPAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnectionNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MaxBitRate" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MaxBitRate" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_FileServer.CertificateEnable" elementDefinition="InternetGatewayDevice.X_ZTE-COM_FileServer.CertificateEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_FileServer.CertificateEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.MTU" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.MTU" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.MTU" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BroadcastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BroadcastPacketsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_IGMP.ProxyTableCurrNum" elementDefinition="InternetGatewayDevice.X_ZTE-COM_IGMP.ProxyTableCurrNum" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_IGMP.ProxyTableCurrNum" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalAssociations" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalAssociations" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.PeriodOfFullLoading" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.PeriodOfFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.PeriodOfFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.Queue.{i}.QueueStatus" elementDefinition="InternetGatewayDevice.QueueManagement.Queue.{i}.QueueStatus" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Firewall.Enable" elementDefinition="InternetGatewayDevice.Firewall.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.Timeout" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.Timeout" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.User.{i}.Enable" elementDefinition="InternetGatewayDevice.User.{i}.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.User.{i}.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_IPv6Enabled" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_IPv6Enabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_IPv6Enabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.AdvOtherConfigFlag" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.AdvOtherConfigFlag" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.AdvOtherConfigFlag" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.URL" elementDefinition="InternetGatewayDevice.ManagementServer.URL" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnicastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnicastPacketsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.MulticastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.MulticastPacketsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPowerSupported" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPowerSupported" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Firewall.Config" elementDefinition="InternetGatewayDevice.Firewall.Config" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.Config" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNServerPort" elementDefinition="InternetGatewayDevice.ManagementServer.STUNServerPort" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.UserClassID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.UserClassID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.SerialNumber" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.SerialNumber" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.SerialNumber" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.PacketsReceived" elementDefinition="InternetGatewayDevice.UDPEchoConfig.PacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.Alias" elementDefinition="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.Alias" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.Alias" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPEncryptionLevel" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPEncryptionLevel" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.Version" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.Version" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.Version" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.XMPP.ConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.XMPP.ConnectionNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.XMPP.ConnectionNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.UploadURL" elementDefinition="InternetGatewayDevice.UploadDiagnostics.UploadURL" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicDataTransmitRates" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicDataTransmitRates" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TestFileLength" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TestFileLength" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDeviceNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDeviceNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKey.{i}.WEPKey" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKey.{i}.WEPKey" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoRateFallBackEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoRateFallBackEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_ServiceControl.IPV4RemoteServicePortControl.{i}.Name" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_ServiceControl.IPV4RemoteServicePortControl.{i}.Name" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_ServiceControl.IPV4RemoteServicePortControl.{i}.Name" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceivedUnderFullLoading" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceivedUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceivedUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_Telnet.CLIUser.Password" elementDefinition="InternetGatewayDevice.X_ZTE-COM_Telnet.CLIUser.Password" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_Telnet.CLIUser.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_DDNS.DomainName" elementDefinition="InternetGatewayDevice.X_ZTE-COM_DDNS.DomainName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_DDNS.DomainName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPLeaseTime" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPLeaseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_MACTable.MacMaxNum" elementDefinition="InternetGatewayDevice.X_ZTE-COM_MACTable.MacMaxNum" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_MACTable.MacMaxNum" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.IPInterface.{i}.LANInterfaceLinkLocalAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.IPInterface.{i}.LANInterfaceLinkLocalAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.IPInterface.{i}.LANInterfaceLinkLocalAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_UPnP.Period" elementDefinition="InternetGatewayDevice.X_ZTE-COM_UPnP.Period" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_UPnP.Period" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Status" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Status" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnectionRequestUsername" elementDefinition="InternetGatewayDevice.ManagementServer.ConnectionRequestUsername" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.AverageResponseTime" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.AverageResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.Enable" elementDefinition="InternetGatewayDevice.Time.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_Clear_Control.DHCPv6" elementDefinition="InternetGatewayDevice.X_ZTE-COM_Clear_Control.DHCPv6" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_Clear_Control.DHCPv6" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceived" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_ALMAC" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_ALMAC" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_ALMAC" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalIntegrityFailures" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalIntegrityFailures" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BeaconType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BeaconType" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.UDPPort" elementDefinition="InternetGatewayDevice.UDPEchoConfig.UDPPort" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.UploadDiagnostics.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_Telnet.CLIUser.Username" elementDefinition="InternetGatewayDevice.X_ZTE-COM_Telnet.CLIUser.Username" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_Telnet.CLIUser.Username" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Parent.Manufacturer" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Parent.Manufacturer" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Parent.Manufacturer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_IGMP.SnoopingEnable" elementDefinition="InternetGatewayDevice.X_ZTE-COM_IGMP.SnoopingEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_IGMP.SnoopingEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Status" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Status" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.Queue.{i}.QueueInterface" elementDefinition="InternetGatewayDevice.QueueManagement.Queue.{i}.QueueInterface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.RadioEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.RadioEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DSCP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.EnableCWMP" elementDefinition="InternetGatewayDevice.ManagementServer.EnableCWMP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.Queue.{i}.QueuePrecedence" elementDefinition="InternetGatewayDevice.QueueManagement.Queue.{i}.QueuePrecedence" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.DiscardPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.DiscardPacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceivedUnderFullLoading" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceivedUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceivedUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_DMZ.Enable" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_DMZ.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_DMZ.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicAuthenticationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicAuthenticationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_ServiceControl.IPV4RemoteServicePortControl.{i}.Port" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_ServiceControl.IPV4RemoteServicePortControl.{i}.Port" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_ServiceControl.IPV4RemoteServicePortControl.{i}.Port" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_DDNS.HostName" elementDefinition="InternetGatewayDevice.X_ZTE-COM_DDNS.HostName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_DDNS.HostName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadTransports" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DownloadTransports" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.DownloadTransports" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.GatewayInfo.ManufacturerOUI" elementDefinition="InternetGatewayDevice.GatewayInfo.ManufacturerOUI" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.GatewayInfo.ManufacturerOUI" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.ModelName" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.ModelName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.ModelName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.DSCP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_APRoaming.RssiThreshold24G" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_APRoaming.RssiThreshold24G" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_APRoaming.RssiThreshold24G" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.AdvManagedFlag" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.AdvManagedFlag" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.AdvManagedFlag" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnectionNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ProductClass" elementDefinition="InternetGatewayDevice.DeviceInfo.ProductClass" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_Mirror.LanInterface" elementDefinition="InternetGatewayDevice.X_ZTE-COM_Mirror.LanInterface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_Mirror.LanInterface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.DefaultConnectionService" elementDefinition="InternetGatewayDevice.Layer3Forwarding.DefaultConnectionService" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.GatewayIPAddress" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.GatewayIPAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_BeaconInterval" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_BeaconInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_BeaconInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.DefaultTrafficClass" elementDefinition="InternetGatewayDevice.QueueManagement.DefaultTrafficClass" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.Interface" elementDefinition="InternetGatewayDevice.UDPEchoConfig.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.STA.{i}.HostName" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.STA.{i}.HostName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.STA.{i}.HostName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.ParameterKey" elementDefinition="InternetGatewayDevice.ManagementServer.ParameterKey" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.InformParameterNumberOfEntries" elementDefinition="InternetGatewayDevice.ManagementServer.InformParameterNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.InformParameterNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MaxBitRate" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BSSID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BSSID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MaxAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MaxAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_URLFilterService.Enable" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_URLFilterService.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_URLFilterService.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TotalBytesSent" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TotalBytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.UploadTransports" elementDefinition="InternetGatewayDevice.UploadDiagnostics.UploadTransports" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.UploadTransports" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.PhysicalLinkStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.PhysicalLinkStatus" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.UpTime" elementDefinition="InternetGatewayDevice.DeviceInfo.UpTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceivedUnderFullLoading" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceivedUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceivedUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnReqXMPPConnection" elementDefinition="InternetGatewayDevice.ManagementServer.ConnReqXMPPConnection" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.ConnReqXMPPConnection" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.Host" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.Host" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadDiagnosticMaxConnections" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DownloadDiagnosticMaxConnections" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.DownloadDiagnosticMaxConnections" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.Manufacturer" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.Manufacturer" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.Manufacturer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.EchoPlusEnabled" elementDefinition="InternetGatewayDevice.UDPEchoConfig.EchoPlusEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_IGMP.ProxyEnable" elementDefinition="InternetGatewayDevice.X_ZTE-COM_IGMP.ProxyEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_IGMP.ProxyEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.DefaultDSCPMark" elementDefinition="InternetGatewayDevice.QueueManagement.DefaultDSCPMark" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.UpgradesManaged" elementDefinition="InternetGatewayDevice.ManagementServer.UpgradesManaged" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.TotalAgentNumberOfEntries" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.TotalAgentNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.TotalAgentNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.SpecVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.SpecVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Standard" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Standard" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.PreferredLifetime" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.PreferredLifetime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.PreferredLifetime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.PrefixDelegationList" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.PrefixDelegationList" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.PrefixDelegationList" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.Queue.{i}.X_ZTE-COM_Name" elementDefinition="InternetGatewayDevice.QueueManagement.Queue.{i}.X_ZTE-COM_Name" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.QueueManagement.Queue.{i}.X_ZTE-COM_Name" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.Host" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.Host" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_DDNS.Hash" elementDefinition="InternetGatewayDevice.X_ZTE-COM_DDNS.Hash" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_DDNS.Hash" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANWLANConfigurationNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANWLANConfigurationNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.ROMTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.ROMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.EnabledForInternet" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.EnabledForInternet" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigMethodsEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigMethodsEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.GatewayInfo.ProductClass" elementDefinition="InternetGatewayDevice.GatewayInfo.ProductClass" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.GatewayInfo.ProductClass" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.X_ZTE-COM_Protocol" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.X_ZTE-COM_Protocol" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.TraceRouteDiagnostics.X_ZTE-COM_Protocol" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNPassword" elementDefinition="InternetGatewayDevice.ManagementServer.STUNPassword" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Status" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Status" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Status" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.BytesResponded" elementDefinition="InternetGatewayDevice.UDPEchoConfig.BytesResponded" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ModemFirmwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.ModemFirmwareVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TestBytesSentUnderFullLoading" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TestBytesSentUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TestBytesSentUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.Queue.{i}.QueueEnable" elementDefinition="InternetGatewayDevice.QueueManagement.Queue.{i}.QueueEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.Prefix" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.Prefix" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.Prefix" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.PacketsResponded" elementDefinition="InternetGatewayDevice.UDPEchoConfig.PacketsResponded" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_RTSThreshold" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_RTSThreshold" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_RTSThreshold" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.Queue.{i}.SchedulerAlgorithm" elementDefinition="InternetGatewayDevice.QueueManagement.Queue.{i}.SchedulerAlgorithm" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.SIPEnable" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.SIPEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.SIPEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.PolicerNumberOfEntries" elementDefinition="InternetGatewayDevice.QueueManagement.PolicerNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.Autonomous" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.Autonomous" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.Autonomous" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.CWMPRetryIntervalMultiplier" elementDefinition="InternetGatewayDevice.ManagementServer.CWMPRetryIntervalMultiplier" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.CWMPRetryIntervalMultiplier" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.MaxPolicerEntries" elementDefinition="InternetGatewayDevice.QueueManagement.MaxPolicerEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.Interface" elementDefinition="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.MinRtrAdvInterval" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.MinRtrAdvInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.MinRtrAdvInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.InterfaceType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.InterfaceType" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.UseAllocatedWAN" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.UseAllocatedWAN" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadURL" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DownloadURL" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.Role" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.Role" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.Role" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.PortControlv6.{i}.DHCPv6" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.PortControlv6.{i}.DHCPv6" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.PortControlv6.{i}.DHCPv6" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.DiscardPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.DiscardPacketsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterfaceNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPower" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPower" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.Enable" elementDefinition="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_ExternelChannel" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_ExternelChannel" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_ExternelChannel" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNEnable" elementDefinition="InternetGatewayDevice.ManagementServer.STUNEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.PHYRate" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.PHYRate" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.PHYRate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPRouters" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPRouters" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.PeriodOfFullLoading" elementDefinition="InternetGatewayDevice.UploadDiagnostics.PeriodOfFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.PeriodOfFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.MTU" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.MTU" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_MaximumClients" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_MaximumClients" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_MaximumClients" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.Enable" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPacketsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_SGI" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_SGI" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_SGI" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_DoS.Anti-PortScan.Enable" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_DoS.Anti-PortScan.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_DoS.Anti-PortScan.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnicastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnicastPacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1UpstreamMaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1UpstreamMaxBitRate" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAEncryptionModes" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAEncryptionModes" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalBytesSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalBytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.ReservedAddresses" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.ReservedAddresses" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Controller.ModelName" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Controller.ModelName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Controller.ModelName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.Version" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.Version" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.Version" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.Origin" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.Origin" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.Origin" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAAuthenticationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAAuthenticationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_MACTable.MacCurrNum" elementDefinition="InternetGatewayDevice.X_ZTE-COM_MACTable.MacCurrNum" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_MACTable.MacCurrNum" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.VendorClassID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.VendorClassID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_VersionSyn.Enable" elementDefinition="InternetGatewayDevice.X_ZTE-COM_VersionSyn.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_VersionSyn.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.HopToController" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.HopToController" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.HopToController" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_APRoaming.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_APRoaming.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_APRoaming.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnectionRequestURL" elementDefinition="InternetGatewayDevice.ManagementServer.ConnectionRequestURL" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_Clear_Control.PPPoE" elementDefinition="InternetGatewayDevice.X_ZTE-COM_Clear_Control.PPPoE" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_Clear_Control.PPPoE" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.ChannelsInUse" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.ChannelsInUse" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.Active" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.Active" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.STA.{i}.IPv4Address" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.STA.{i}.IPv4Address" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.STA.{i}.IPv4Address" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.Interface" elementDefinition="InternetGatewayDevice.UploadDiagnostics.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.PrefixDelegationList" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.PrefixDelegationList" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.PrefixDelegationList" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenResponseTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TCPOpenResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.CurrentLocalTime" elementDefinition="InternetGatewayDevice.Time.CurrentLocalTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.NumberOfActiveConnections" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.NumberOfActiveConnections" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerConfigurable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerConfigurable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.PacketErrorsRX" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.PacketErrorsRX" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.PacketErrorsRX" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_IGMP.SnoopingEnhancementEnable" elementDefinition="InternetGatewayDevice.X_ZTE-COM_IGMP.SnoopingEnhancementEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_IGMP.SnoopingEnhancementEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.DestIPAddress" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.DestIPAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.Status" elementDefinition="InternetGatewayDevice.Time.Status" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Status" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Status" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_IGMP.PortSnoopingTable.{i}.SnoopingTableMaxNum" elementDefinition="InternetGatewayDevice.X_ZTE-COM_IGMP.PortSnoopingTable.{i}.SnoopingTableMaxNum" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_IGMP.PortSnoopingTable.{i}.SnoopingTableMaxNum" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BeaconAdvertisementEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BeaconAdvertisementEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Syslog.Level" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Syslog.Level" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Syslog.Level" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.TotalSTANumberOfEntries" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.TotalSTANumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.TotalSTANumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_UPnP.Enable" elementDefinition="InternetGatewayDevice.X_ZTE-COM_UPnP.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_UPnP.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.DSCP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Controller.Manufacturer" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Controller.Manufacturer" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Controller.Manufacturer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_DDNS.Username" elementDefinition="InternetGatewayDevice.X_ZTE-COM_DDNS.Username" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_DDNS.Username" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.Queue.{i}.QueueBufferLength" elementDefinition="InternetGatewayDevice.QueueManagement.Queue.{i}.QueueBufferLength" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Securitylog.Enable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Securitylog.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Securitylog.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigMethodsSupported" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigMethodsSupported" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MaxBitRate" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MaxBitRate" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.MACAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.MACAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPSKFailures" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPSKFailures" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.Enable" elementDefinition="InternetGatewayDevice.QueueManagement.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.PacketErrorsTX" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.PacketErrorsTX" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.PacketErrorsTX" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_BandSteering.BsRssiLmt5G" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_BandSteering.BsRssiLmt5G" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_BandSteering.BsRssiLmt5G" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.HostName" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.HostName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Parent.AL_MAC" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Parent.AL_MAC" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Parent.AL_MAC" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.NTPServer5" elementDefinition="InternetGatewayDevice.Time.NTPServer5" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_DDNS.Provider" elementDefinition="InternetGatewayDevice.X_ZTE-COM_DDNS.Provider" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_DDNS.Provider" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.ManufacturerOUI" elementDefinition="InternetGatewayDevice.DeviceInfo.ManufacturerOUI" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.NTPServer1" elementDefinition="InternetGatewayDevice.Time.NTPServer1" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.ROMTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.ROMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.NTPServer2" elementDefinition="InternetGatewayDevice.Time.NTPServer2" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.WANAccessType" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.WANAccessType" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.NTPServer3" elementDefinition="InternetGatewayDevice.Time.NTPServer3" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.NTPServer4" elementDefinition="InternetGatewayDevice.Time.NTPServer4" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_Telnet.Enable" elementDefinition="InternetGatewayDevice.X_ZTE-COM_Telnet.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_Telnet.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.StaticRoute" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.StaticRoute" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSent" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.DnsRefreshTime" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.DnsRefreshTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.DnsRefreshTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.MulticastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.MulticastPacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iAuthenticationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iAuthenticationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.L2TPEnable" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.L2TPEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.L2TPEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.SignalStrength" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.SignalStrength" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.SignalStrength" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.ManualDNSEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.ManualDNSEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.ManualDNSEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.NATDetected" elementDefinition="InternetGatewayDevice.ManagementServer.NATDetected" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.ForwardNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer3Forwarding.ForwardNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnectionRequestPassword" elementDefinition="InternetGatewayDevice.ManagementServer.ConnectionRequestPassword" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnknownProtoPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnknownProtoPacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.X_ZTE-COM_CertificateEnable" elementDefinition="InternetGatewayDevice.ManagementServer.X_ZTE-COM_CertificateEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.X_ZTE-COM_CertificateEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.PortControlv6.{i}.RA" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.PortControlv6.{i}.RA" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.PortControlv6.{i}.RA" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MACAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MACAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.QueueNumberOfEntries" elementDefinition="InternetGatewayDevice.QueueManagement.QueueNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.BytesReceived" elementDefinition="InternetGatewayDevice.UDPEchoConfig.BytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TotalBytesSentUnderFullLoading" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TotalBytesSentUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TotalBytesSentUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenRequestTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TCPOpenRequestTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.Queue.{i}.ShapingRate" elementDefinition="InternetGatewayDevice.QueueManagement.Queue.{i}.ShapingRate" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.Origin" elementDefinition="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.Origin" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.Origin" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TestBytesSent" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TestBytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TestBytesSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Remotelog.Enable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Remotelog.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Remotelog.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.PerConnectionResultNumberOfEntries" elementDefinition="InternetGatewayDevice.UploadDiagnostics.PerConnectionResultNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.PerConnectionResultNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.NumberOfConnections" elementDefinition="InternetGatewayDevice.UploadDiagnostics.NumberOfConnections" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.NumberOfConnections" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.Queue.{i}.TrafficClasses" elementDefinition="InternetGatewayDevice.QueueManagement.Queue.{i}.TrafficClasses" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.MaxQueueEntries" elementDefinition="InternetGatewayDevice.QueueManagement.MaxQueueEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_URLFilterService.Mode" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_URLFilterService.Mode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_URLFilterService.Mode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceSubnetMask" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceSubnetMask" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSIDAdvertisementEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSIDAdvertisementEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.BOMTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.BOMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.RegulatoryDomain" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.RegulatoryDomain" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Syslog.Enable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Syslog.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Syslog.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.LeaseTimeRemaining" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.LeaseTimeRemaining" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.PeriodicInformEnable" elementDefinition="InternetGatewayDevice.ManagementServer.PeriodicInformEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.MediaType" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.MediaType" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.MediaType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.EOMTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.EOMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceSummary" elementDefinition="InternetGatewayDevice.DeviceSummary" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BroadcastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BroadcastPacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnReqJabberID" elementDefinition="InternetGatewayDevice.ManagementServer.ConnReqJabberID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.ConnReqJabberID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.AL_MAC" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.AL_MAC" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.NetworkTopology.Controller.AL_MAC" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.EthernetPriority" elementDefinition="InternetGatewayDevice.UploadDiagnostics.EthernetPriority" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.DefaultEthernetPriorityMark" elementDefinition="InternetGatewayDevice.QueueManagement.DefaultEthernetPriorityMark" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_DMZ.LanHost" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_DMZ.LanHost" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_DMZ.LanHost" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Name" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Name" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.ParentPrefix" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.ParentPrefix" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.ParentPrefix" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_IGMP.PortSnoopingTable.{i}.Port" elementDefinition="InternetGatewayDevice.X_ZTE-COM_IGMP.PortSnoopingTable.{i}.Port" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_IGMP.PortSnoopingTable.{i}.Port" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNMaximumKeepAlivePeriod" elementDefinition="InternetGatewayDevice.ManagementServer.STUNMaximumKeepAlivePeriod" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.DestSubnetMask" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.DestSubnetMask" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_Telnet.Port" elementDefinition="InternetGatewayDevice.X_ZTE-COM_Telnet.Port" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_Telnet.Port" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Parent.SerialNumber" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Parent.SerialNumber" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Parent.SerialNumber" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.SerialNumber" elementDefinition="InternetGatewayDevice.DeviceInfo.SerialNumber" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_AccessControlMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_AccessControlMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_AccessControlMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Parent.ModelName" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Parent.ModelName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Parent.ModelName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNServerAddress" elementDefinition="InternetGatewayDevice.ManagementServer.STUNServerAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.Interface" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.Timeout" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.Timeout" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.Password" elementDefinition="InternetGatewayDevice.ManagementServer.Password" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.PerConnectionResultNumberOfEntries" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.PerConnectionResultNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.PerConnectionResultNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.ForwardingMetric" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.ForwardingMetric" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.Manufacturer" elementDefinition="InternetGatewayDevice.DeviceInfo.Manufacturer" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.DevicePassword" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.DevicePassword" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.PeriodicInformTime" elementDefinition="InternetGatewayDevice.ManagementServer.PeriodicInformTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.MinimumResponseTime" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.MinimumResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceAddressingType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceAddressingType" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.X_AcsPeriodicInformInterval" elementDefinition="InternetGatewayDevice.ManagementServer.X_AcsPeriodicInformInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.X_AcsPeriodicInformInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_DDNS.Password" elementDefinition="InternetGatewayDevice.X_ZTE-COM_DDNS.Password" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_DDNS.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_DoS.Anti-PortScan.Threshold" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_DoS.Anti-PortScan.Threshold" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_DoS.Anti-PortScan.Threshold" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicEncryptionModes" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicEncryptionModes" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Controller.SerialNumber" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Controller.SerialNumber" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Controller.SerialNumber" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_IGMP.ProxyTableMaxNum" elementDefinition="InternetGatewayDevice.X_ZTE-COM_IGMP.ProxyTableMaxNum" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_IGMP.ProxyTableMaxNum" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1DownstreamMaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1DownstreamMaxBitRate" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PreSharedKey.{i}.KeyPassphrase" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PreSharedKey.{i}.KeyPassphrase" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceived" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.RTSPEnable" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.RTSPEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.RTSPEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DNS.X_ZTE-COM_IPv4DNSServer2" elementDefinition="InternetGatewayDevice.DNS.X_ZTE-COM_IPv4DNSServer2" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DNS.X_ZTE-COM_IPv4DNSServer2" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.FirstUseDate" elementDefinition="InternetGatewayDevice.DeviceInfo.FirstUseDate" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.DNSAddress1" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.DNSAddress1" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.DNSAddress1" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.DNSAddress2" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.DNSAddress2" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.DNSAddress2" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.NumberOfConnections" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.NumberOfConnections" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.NumberOfConnections" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Channel" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Channel" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.DNSAddress3" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.DNSAddress3" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.DHCPv6.DNSAddress3" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.User.{i}.Username" elementDefinition="InternetGatewayDevice.User.{i}.Username" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.User.{i}.Username" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.Interface" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Controller.AL_MAC" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Controller.AL_MAC" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Controller.AL_MAC" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.ProvisioningCode" elementDefinition="InternetGatewayDevice.DeviceInfo.ProvisioningCode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DNS.X_ZTE-COM_IPv4DNSServer1" elementDefinition="InternetGatewayDevice.DNS.X_ZTE-COM_IPv4DNSServer1" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DNS.X_ZTE-COM_IPv4DNSServer1" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.X_ZTE-COM_Alias" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.X_ZTE-COM_Alias" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.X_ZTE-COM_Alias" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MACAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MACAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.FTPEnable" elementDefinition="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.FTPEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Firewall.X_ZTE-COM_ALG.FTPEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.EthernetPriority" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.EthernetPriority" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Interface" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_IGMP.PortSnoopingTable.{i}.SnoopingTableCurNum" elementDefinition="InternetGatewayDevice.X_ZTE-COM_IGMP.PortSnoopingTable.{i}.SnoopingTableCurNum" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_IGMP.PortSnoopingTable.{i}.SnoopingTableCurNum" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TCPOpenRequestTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TCPOpenRequestTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.IPAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.IPAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_SSIDIsolation" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_SSIDIsolation" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_SSIDIsolation" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalBytesReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalBytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iEncryptionModes" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iEncryptionModes" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.DuplexMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.DuplexMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.HostNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.HostNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.SubnetMask" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.SubnetMask" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddressNotificationLimit" elementDefinition="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddressNotificationLimit" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.PrefixDelegationType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.PrefixDelegationType" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.PrefixDelegationType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_BandSteering.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_BandSteering.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_BandSteering.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_APRoaming.RssiThreshold5G" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_APRoaming.RssiThreshold5G" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_APRoaming.RssiThreshold5G" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.TimeLastPacketReceived" elementDefinition="InternetGatewayDevice.UDPEchoConfig.TimeLastPacketReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.ResponseTime" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.ResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.OnLink" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.OnLink" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.Prefix.{i}.OnLink" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.PortControlv6.{i}.LanInterfaceName" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.PortControlv6.{i}.LanInterfaceName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.PortControlv6.{i}.LanInterfaceName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Enable" elementDefinition="InternetGatewayDevice.Layer3Forwarding.Forwarding.{i}.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ZTE-COM_ISPDNSEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ZTE-COM_ISPDNSEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ZTE-COM_ISPDNSEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_BandSteering.BsRssiLmt24G" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_BandSteering.BsRssiLmt24G" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_BandSteering.BsRssiLmt24G" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNMinimumKeepAlivePeriod" elementDefinition="InternetGatewayDevice.ManagementServer.STUNMinimumKeepAlivePeriod" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.KeyPassphrase" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.KeyPassphrase" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ModelName" elementDefinition="InternetGatewayDevice.DeviceInfo.ModelName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceIPAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceIPAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_WlanStandard" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_WlanStandard" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ZTE-COM_WlanStandard" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.PacketsTX" elementDefinition="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.PacketsTX" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_EasyMesh.MeshAgent.Backhaul.PacketsTX" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.CWMPRetryMinimumWaitInterval" elementDefinition="InternetGatewayDevice.ManagementServer.CWMPRetryMinimumWaitInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.CWMPRetryMinimumWaitInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_MLD.ProxyEnable" elementDefinition="InternetGatewayDevice.X_ZTE-COM_MLD.ProxyEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_MLD.ProxyEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPRelay" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPRelay" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.AllowedMACAddresses" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.AllowedMACAddresses" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MinAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MinAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_Mesh.MeshEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_Mesh.MeshEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_Mesh.MeshEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.Description" elementDefinition="InternetGatewayDevice.DeviceInfo.Description" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ZTE-COM_UPnP.TTL" elementDefinition="InternetGatewayDevice.X_ZTE-COM_UPnP.TTL" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ZTE-COM_UPnP.TTL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.EchoPlusSupported" elementDefinition="InternetGatewayDevice.UDPEchoConfig.EchoPlusSupported" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Alias" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Alias" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ZTE-COM_Alias" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.RouteHopsNumberOfEntries" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.RouteHopsNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.PrefixLen" elementDefinition="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.PrefixLen" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Layer3Forwarding.X_ZTE-COM_IPv6Forwarding.{i}.PrefixLen" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.Queue.{i}.DefaultQueue" elementDefinition="InternetGatewayDevice.QueueManagement.Queue.{i}.DefaultQueue" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.QueueManagement.Queue.{i}.DefaultQueue" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.Preference" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.Preference" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ZTE-COM_IPv6LANHostConfigManagement.RAConfigManagement.Preference" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Status" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Status" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.AddressSource" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.Host.{i}.AddressSource" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.DefaultPolicer" elementDefinition="InternetGatewayDevice.QueueManagement.DefaultPolicer" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TCPOpenResponseTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TCPOpenResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.SupportedConnReqMethods" elementDefinition="InternetGatewayDevice.ManagementServer.SupportedConnReqMethods" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.SupportedConnReqMethods" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.FailureCount" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.FailureCount" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.DownloadDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="Download Diagnostics" subType="DOWNLOADSPEED">
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadURL" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.Interface" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.DSCP" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.EthernetPriority" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.EOMTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.ROMTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceived"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceived"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.BOMTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenRequestTime"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.IPPingDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="IP Ping Diagnostics" subType="IPPING">
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.DSCP" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.Host" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.DataBlockSize" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.Timeout" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.Interface" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.FailureCount"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.AverageResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.MaximumResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.MinimumResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.SuccessCount"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.TraceRouteDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="TraceRoute Diagnostics" subType="TRACEROUTE">
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.Interface" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.Timeout" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.DSCP" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.Host" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.TraceRouteDiagnostics.RouteHopsNumberOfEntries"/>
        <returnParameterNames name="InternetGatewayDevice.TraceRouteDiagnostics.ResponseTime"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.UploadDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="Upload Diagnostics" subType="UPLOADSPEED">
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.DSCP" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.TestFileLength" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.Interface" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.UploadURL" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.EthernetPriority" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.EOMTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.BOMTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.TCPOpenRequestTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.TotalBytesSent"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.ROMTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.TCPOpenResponseTime"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 2" description="network interface definition">
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.SSID" parameterType="SSID"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Status" parameterType="OTHER"/>
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.BSSID" parameterType="OTHER"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Enable" parameterType="OTHER"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.TotalBytesSent" parameterType="BYTES_SENT"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 1" description="network interface definition">
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.BSSID" parameterType="OTHER"/>
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Status" parameterType="OTHER"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Enable" parameterType="OTHER"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.TotalBytesSent" parameterType="BYTES_SENT"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.SSID" parameterType="SSID"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="Ethernet" name="Ethernet 2" description="network interface definition">
        <properties name="MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.MACAddress" parameterType="MAC_ADDRESS"/>
        <properties name="Port Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.Stats.BytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Port Bytes sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.Stats.BytesSent" parameterType="BYTES_SENT"/>
        <properties name="Port Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.Status" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 3" description="network interface definition">
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.3.SSID" parameterType="SSID"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.3.Enable" parameterType="OTHER"/>
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.3.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.3.TotalBytesSent" parameterType="BYTES_SENT"/>
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.3.BSSID" parameterType="OTHER"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.3.Status" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="Ethernet" name="Ethernet 1" description="network interface definition">
        <properties name="Port Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.Stats.BytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Port Bytes sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.Stats.BytesSent" parameterType="BYTES_SENT"/>
        <properties name="Port Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.Status" parameterType="OTHER"/>
        <properties name="MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.MACAddress" parameterType="MAC_ADDRESS"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 5" description="network interface definition">
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Status" parameterType="OTHER"/>
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Enable" parameterType="OTHER"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.SSID" parameterType="SSID"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.TotalBytesSent" parameterType="BYTES_SENT"/>
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.BSSID" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 6" description="network interface definition">
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.6.Enable" parameterType="OTHER"/>
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.6.BSSID" parameterType="OTHER"/>
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.6.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.6.TotalBytesSent" parameterType="BYTES_SENT"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.6.SSID" parameterType="SSID"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.6.Status" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 4" description="network interface definition">
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.4.BSSID" parameterType="OTHER"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.4.SSID" parameterType="SSID"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.4.TotalBytesSent" parameterType="BYTES_SENT"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.4.Status" parameterType="OTHER"/>
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.4.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.4.Enable" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 7" description="network interface definition">
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.7.TotalBytesSent" parameterType="BYTES_SENT"/>
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.7.BSSID" parameterType="OTHER"/>
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.7.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.7.Enable" parameterType="OTHER"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.7.Status" parameterType="OTHER"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.7.SSID" parameterType="SSID"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 8" description="network interface definition">
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.8.BSSID" parameterType="OTHER"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.8.Enable" parameterType="OTHER"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.8.SSID" parameterType="SSID"/>
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.8.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.8.Status" parameterType="OTHER"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.8.TotalBytesSent" parameterType="BYTES_SENT"/>
    </deviceModelNetworkInterfaces>
</DeviceModel>
