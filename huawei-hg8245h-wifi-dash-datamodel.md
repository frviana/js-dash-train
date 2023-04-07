<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<DeviceModel name="Huawei-HG8245H-LIGAVC" manufacturer="Huawei-HG8245H-LIGAVC" oui="00259E" productClass="HG8145V5" objectModelDefinitions="InternetGatewayDevice:1.4 VoiceService:1.0" softwareVersions="EDIT ME(8)" description="" setNotification="true" setAccessList="true" protocolType="TR069">
    <supportedRPCMethods>DeleteObject</supportedRPCMethods>
    <supportedRPCMethods>TransferComplete</supportedRPCMethods>
    <supportedRPCMethods>GetParameterNames</supportedRPCMethods>
    <supportedRPCMethods>GetQueuedTransfers</supportedRPCMethods>
    <supportedRPCMethods>GetParameterAttributes</supportedRPCMethods>
    <supportedRPCMethods>RequestDownload</supportedRPCMethods>
    <supportedRPCMethods>Upload</supportedRPCMethods>
    <supportedRPCMethods>AddObject</supportedRPCMethods>
    <supportedRPCMethods>GetParameterValues</supportedRPCMethods>
    <supportedRPCMethods>Reboot</supportedRPCMethods>
    <supportedRPCMethods>SetParameterAttributes</supportedRPCMethods>
    <supportedRPCMethods>GetRPCMethods</supportedRPCMethods>
    <supportedRPCMethods>GetAllQueuedTransfers</supportedRPCMethods>
    <supportedRPCMethods>ScheduleDownload</supportedRPCMethods>
    <supportedRPCMethods>ScheduleInform</supportedRPCMethods>
    <supportedRPCMethods>X_HW_GetParamValuesEagerly</supportedRPCMethods>
    <supportedRPCMethods>ChangeDUState</supportedRPCMethods>
    <supportedRPCMethods>SetParameterValues</supportedRPCMethods>
    <supportedRPCMethods>Download</supportedRPCMethods>
    <supportedRPCMethods>FactoryReset</supportedRPCMethods>
    <options discoveryAlgorithmType="BATCH_DISCOVERY" dashboardDevicePollTime="10" reloadOnFactoryReset="NEVER" collectConnectedDevices="false" addObjectBackfill="true" discoveryRetry="0" simpleDiscoveryRetry="3" simpleDiscoveryEnabled="false"/>
    <deviceServiceConfigurations name="TR-69 Config">
        <scriptDefinition name="Huawei-HG8245Q2-LIGAVC(1):TR-69 Config" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
        <scriptDefinition name="Huawei-HG8245Q2-LIGAVC(1):DHCP" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="Device Log">
        <scriptDefinition name="Huawei-HG8245Q2-LIGAVC(1):Device Log" purpose="Device service configuration" tags="null" scriptParameters="[]">
            <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var deviceId = scriptParameters.deviceId;
var response = dsc.getDeviceParameterLogs(deviceId);

response;
</javaScriptCode>
        </scriptDefinition>
    </deviceServiceConfigurations>
    <deviceServiceConfigurations name="WiFi 5">
        <scriptDefinition name="Huawei-HG8245Q2-LIGAVC(1):WiFi 5" purpose="Device service configuration" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
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
    <deviceServiceConfigurations name="WiFi5Ghz">
        <scriptDefinition name="Huawei-HG8245Q2-LIGAVC(1):WiFi5Ghz" purpose="Device service configuration" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
            <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var channelDataType = {
  type: "ENUM", 
  choice:[
    //{ systemName: "0", friendlyName: "auto" },
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
    { name:"ssid", label: "##wifi.ssid##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.SSID" },
    { name:"enabled", label: "##wifi.wifi_enable##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Enable" },
    { name:"broadcastSsid", label: "##wifi.broadcast_ssid##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.BeaconAdvertisementEnabled" },
    { name:"channel", label: "##wifi.channel##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Channel", dataType: channelDataType },
    /**{ name:"channelWidth",label: "##wifi.channel_width##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.X_000E50_ChannelWidth", dataType: channelWidthDataType },**/
    { name: "transmitPower",label: "##wifi.transmit_power##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.TransmitPower", dataType: transmitPowerDataType },
    { name: "frequency", label: "##wifi.frequency##", description: "Frequency", value:"5GHz",  writable: false },
    { name:"passwordIndex", label: "##wifi.password_index##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.WEPKeyIndex", groups: ["WEP-Open", "WEP-Shared"] },
    { name:"password1", label: "Password 1", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.WEPKey.1.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: passwordDataType, groups: ["WEP-Open", "WEP-Shared"], readCallback: readPassword },
    { label: "Password 2", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.WEPKey.2.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    { label: "Password 3", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.WEPKey.3.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    { label: "Password 4", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.WEPKey.4.WEPKey", description: "5 chars for 64bit and 13 chars for 128bit", dataType: { type: "PASSWORD", "min": 0, "max": 13 }, groups: ["WEP-Open", "WEP-Shared"] },
    /*{ name:"password", label: "##wifi.password##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.PreSharedKey.1.KeyPassphrase", group: "WPA", dataType: passwordDataType },*/
    { name:"password", label: "##wifi.password##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.PreSharedKey.1.KeyPassphrase", groups: ["Disabled","WEP-Open", "WEP-Shared", "WPA"], dataType: passwordDataType, readCallback: readPassword },
    { label: "WPA Authentication Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.WPAAuthenticationMode", internalOnly: true },
    { label: "WPA Encryption Modes", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.WPAEncryptionModes", internalOnly: true },
    { label: "Basic Authentication Mode", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.BasicAuthenticationMode", internalOnly: true },
    { label: "Basic Encryption Modes", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.BasicEncryptionModes", internalOnly: true },
    { label: "Beacon Type", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.BeaconType", internalOnly: true },
    { label: "Standard", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Standard", internalOnly: true },
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
    <deviceServiceConfigurations name="WiFi 2">
        <scriptDefinition name="Huawei-HG8245Q2-LIGAVC(1):WiFi 2" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="WiFi24Ghz">
        <scriptDefinition name="Huawei-HG8245Q2-LIGAVC(1):WiFi24Ghz" purpose="Device service configuration" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
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
      case "Password":
        if(scriptParameters.Password.length &lt; 8) {
          throw "Password length invalid. Must be 8-63 ASCII characters";
        }
        cpeParameters.Password.value = scriptParameters.Password;
        cpeParameters.Password.updated = true;
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
        <scriptDefinition name="Huawei-HG8245Q2-LIGAVC(1):WiFi 1" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="WAN">
        <scriptDefinition name="Huawei-HG8245Q2-LIGAVC(1):WAN" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceActions name="Run diagnostic">
        <scriptDefinition name="Huawei-HG8245Q2-LIGAVC(1):Run diagnostic" purpose="Device service configuration" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
            <javaScriptCode>var acs = require("acs");
var body = {
    operations: []
};
var deviceId=scriptParameters.deviceId;

 

var op = {
  operationType: "SETPARAMETERVALUE",
  operationParameters: []
};
op.operationParameters.push({
  name: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel",
  value: "0"
});
op.operationParameters.push({
  name: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.AutoChannelEnable",
  value: "false"
});
op.operationParameters.push({
  name: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel",
  value: "0"
});
op.operationParameters.push({
  name: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.AutoChannelEnable",
  value: "false"
});

 


body.operations.push(op);
op = {
  operationType: "SETPARAMETERVALUE",
  operationParameters: []
};
op.operationParameters.push({
  name: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.AutoChannelEnable",
  value: "true"
});
op.operationParameters.push({
  name: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.AutoChannelEnable",
  value: "true"
});

 

body.operations.push(op);

 

var op = acs.createUserDefinedOperation(body, deviceId);
var result = {deviceOperationIds:[op.id]};
result;</javaScriptCode>
        </scriptDefinition>
    </deviceActions>
    <deviceLogParameters name="Device Log 1" parameterName="InternetGatewayDevice.DeviceInfo.DeviceLog"/>
    <dataComposers name="Bytes Received">
        <scriptDefinition name="Huawei-HG8245Q2-LIGAVC(1):Bytes Received" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
        <scriptDefinition name="Huawei-HG8245Q2-LIGAVC(1):Bytes Sent" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
        <scriptDefinition name="Huawei-HG8245Q2-LIGAVC(1):Memoria Livre" purpose="Device service configuration" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
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
    <dashboardPanelScripts>
        <dashboardPanelScript name="Connected Devices Topology" scriptType="DASHBOARD_SCRIPT">
            <scriptDefinition name="Huawei:Connected Devices Topology(1)(1)(1)" purpose="Device service configuration" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
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
    //{ name: "SignalStrength", label: "Signal Strength", cpeParameterName: "InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SignalStrength" },
    { name: "SignalStrength", label: "Signal Strength", cpeParameterName: "Device.X_Incognito.ConnectedDevices.Host.{i}.X_HW_RSSI" },
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
        <dashboardPanelScript name="Automated Troubleshooting" scriptType="DASHBOARD_SCRIPT">
            <scriptDefinition name="Huawei Oficial:Automated Troubleshooting(1)(1)(1)" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
                <javaScriptCode>/**
 * NOTE: This auto generated script is populated with out of the box parameters. 
 *       Please ensure the parameters in the script matches the proper device parameters.
 * This script runs a series of tests to troubleshoot WiFi connectivity issues
 * It runs the following set of tests as part of the troubleshooting process
 * 1. Check if Wifi 2.4GHz is enabled
 * 2. Check if Wifi 5GHz is enabled
 * 3. Check if signal strength of the connected devices are above a certain threshold
 * 4. Check for interference in the channel used by Wifi
 * 5. Check if upload speed is above a certain threshold
 *    NOTE: Threshold is set to an arbitrary number in the script.
 * 6. check if download speed is above a certain threshold 
 *    NOTE: Threshold is set to an arbitrary number in the script.
 * 7. Check if the number of connected devices is above a certain threshold
 *    NOTE: Threshold is set to an arbitrary number in the script.
 * 
 * If there is no wifi connection (both Wifi 2.4GHz and 5GHz are disabled), rest of the tests are skipped.
 */

var acs = require('acs');
var ts = require('guidedtroubleshooting');

var wifi24GParamName = "Wifi24G";
var wifi5GParamName = "Wifi5G";
var signalStrengthParamName = "signal-strength";
var channel24GParamName = "channel24G";
var channel5GParamName = "channel5G";
var autoChannel24GParamName = "autoChannel24G";
var autochannel5GParamName = "autoChannel5G";

/**
 * Parameters to run the troubleshooting tests.
 * These parameters should match the device parameters.
 */
var testParameters = [
  //Device Parameter to check if Wifi 2.4GHz is enabled
  { name: wifi24GParamName, label: "##Wifi.24G.enabled##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Enable" },
  //Device Parameter to check if Wifi 5GHz is enabled
  { name: wifi5GParamName, label: "##Wifi.5G.enabled##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Enable" },
  //Device Parameter to get the current channel Wifi 2.4GHz uses
  { name: channel24GParamName, label: "##wifi.24G.channel##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel" },
  //Device Parameter to get the current channel Wifi 5GHz uses
  { name: channel5GParamName, label: "##wifi.5G.channel##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel" },
  //Device Parameter to check if Wifi 2.4GHz uses Auto channel
  { name: autoChannel24GParamName, label: "##wifi.24G.autochannel##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.AutoChannelEnable" },
  //Device Parameter to check if Wifi 5GHz uses Auto channel
  { name: autochannel5GParamName, label: "##wifi.5G.autochannel##", cpeParameterName: "InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.AutoChannelEnable" }
];

//Threshold values to test against
//Upload speed mininum threshold value
const UPLOADSPEED_MIN_THRESHOLD_IN_MBPS = 0.0;
//Download speed minimum threshold value
const DOWNLOADSPEED_MIN_THRESHOLD_IN_MBPS = 0;
//connected devices minimum threshold value
const CONNECTEDDEVICES_MIN_THRESHOLD = 5;
//Connected devices maximum threshold value
const CONNECTEDDEVICES_MAX_THRESHOLD = 10;
//Connected devices minimum signal strenght
const CONNECTEDDEVICES_MIN_SIGNALSTRENGTH_IN_MBPS = -70;

/**
 * JSON body to run upload and download speed tests.
 * Please make sure the diagnostics input parameters match the device parameters
 */
var speedTestBody = {
  operations: [
    {
      operationType: "DIAGNOSTICS",
      operationParameters: [
        {
          name: "DIAGNOSTIC_OPERATION",
          value: "DOWNLOADSPEED"
        },
        {
          name: "InternetGatewayDevice.DownloadDiagnostics.DownloadURL",
          value: "http://35.215.210.14:9090/download.bin"
        }
      ]
    },
    {
      operationType: "DIAGNOSTICS",
      operationParameters: [
        {
          name: "DIAGNOSTIC_OPERATION",
          value: "UPLOADSPEED"
        },
        {
          name: "InternetGatewayDevice.UploadDiagnostics.UploadURL",
          value: "http://35.215.210.14:9090/upload.bin"
        },
        {
          name: "InternetGatewayDevice.UploadDiagnostics.TestFileLength",
          value: "10000"
        }
      ]
    }
  ]
};

var tests = {
  wifi24GTest: "Wifi24GHz",
  wifi5GTest: "Wifi5GHz",
  signalStrengthTest: "WifiSignalStrength",
  interferenceTest: "WifiInterference",
  uploadSpeedTest: "uploadSpeedTest",
  downloadSpeedTest: "downloadSpeedTest",
  connectedDevicesCount: "connectedDevices",
  softwareVersionTest: "firmwareVersion"
};

function is24GEnabled(isWifi24GEnabled) {
  publishInProgressResponse(tests.wifi24GTest);

  if (isWifi24GEnabled === null) {
    ts.setCompletedWithErrorsStatus();
    ts.setMessage("Wifi setting not found");
    ts.addComments("Unable to run the test", "No wifi setting found");
    ts.addActionTitle("Test incomplete");
    ts.addActionListItem(["Unable to read Wifi band value", "Relevant device parameters not found"]);
  } else {
    if (isWifi24GEnabled === 'nullValue' || isWifi24GEnabled === '0' || isWifi24GEnabled === 'false' || isWifi24GEnabled === false) {
      ts.setCompletedWithErrorsStatus();
      ts.setMessage("Disabled");
      ts.addComments("Enable 2.4GHz Band", "Enabling 2.4GHz will provide better range. For better bandwidth, check if 5Ghz is enabled");
      ts.addActionTitle("Enable 2.4GHz band");
      ts.addActionListItem(["Enable 2.4GHz band in ACS", "Confirm with customer that the problem is solved"]);
    } else {
      ts.setCompletedSuccessfulStatus();
      ts.setMessage("Enabled");
    }
  }

  var resp = ts.returnTroubleshootingEventResponse();
  log.info(resp);
  publishMsg(resp);
}

function is5GEnabled(isWifi5GEnabled) {
  publishInProgressResponse(tests.wifi5GTest);

  if (isWifi5GEnabled === null) {
    ts.setCompletedWithErrorsStatus();
    ts.setMessage("Wifi setting not found");
    ts.addComments("Unable to run the test", "No wifi setting found");
    ts.addActionTitle("Test incomplete");
    ts.addActionListItem(["Unable to read Wifi band value", "Relevant device parameters not found"]);
  } else {
    if (isWifi5GEnabled === 'nullValue' || isWifi5GEnabled === '0' || isWifi5GEnabled === 'false' || isWifi5GEnabled === false) {
      ts.setCompletedWithErrorsStatus();
      ts.setMessage("Disabled");
      ts.addComments("Enable 5GHz Band", "If customer has slow internet, using 5GHz band may solve the problem");
      ts.addActionTitle("Enable 5GHz band");
      ts.addActionListItem(["Enable 5GHz band in ACS", "Confirm with customer that the problem is solved"]);
    } else {
      ts.setCompletedSuccessfulStatus();
      ts.setMessage("Enabled");
    }
  }
  var resp = ts.returnTroubleshootingEventResponse();
  log.info(resp);
  publishMsg(resp);
}

function signalStrengthTest(isWifiEnabled) {
  publishInProgressResponse(tests.signalStrengthTest);
  if (isWifiEnabled === false) {
    skipTest(isWifiEnabled);
    return;
  }

  //Perform Test
  var signalStrengths = ts.getConnectedDevicesSignalStrengths(parameterValues, signalStrengthParamName);
  if (signalStrengths === 'undefined' || signalStrengths === null || 0 === signalStrengths.length) {
    ts.setCompletedWithErrorsStatus();
    ts.setMessage("Unable to test connection");
    ts.addComments("Unable to test wifi connection", "Signal strength parameter values of connected devices not found");
    ts.addActionTitle("Unable to test connection");
    ts.addActionListItem(["Unable to test wifi connection", "Signal strength parameter values of connected devices not found"]);
  } else {
    var signalStrengthLow = false;
    for (var i = 0; i &lt; signalStrengths.length; i++) {
      if (signalStrengths[i] &lt;= CONNECTEDDEVICES_MIN_SIGNALSTRENGTH_IN_MBPS) {
        signalStrengthLow = true;
        break;
      }
    }
    if (signalStrengthLow) {
      ts.setCompletedWithErrorsStatus();
      ts.setMessage("Poor connection");
      ts.addComments("Poor wifi connection", "If connection from the device to the router is poor, the customer may have problems accessing the internet.");
      ts.addActionTitle("Enable 5GHz band");
      ts.addActionListItem(["Disable/enable WiFi in ACS",
        "Review with the customer if it is possible to reposition the router or the devices so that they’re closer."]);
    }
    else {
      ts.setCompletedSuccessfulStatus();
      ts.setOkMessage();
    }
  }

  var resp = ts.returnTroubleshootingEventResponse();
  log.info(resp);
  publishMsg(resp);
}

function interferenceTest(parameterValues, isWifiEnabled, isWifi24GEnabled, isWifi5GEnabled) {
  publishInProgressResponse(tests.interferenceTest);
  if (isWifiEnabled === false) {
    skipTest(isWifiEnabled);
    return;
  }

  if (isWifi5GEnabled === 1 || isWifi5GEnabled === '1' || isWifi5GEnabled === true || isWifi5GEnabled === 'true') {
    var autoChannelSetWifi5G = ts.checkAutoChannelSet(parameterValues, autochannel5GParamName);
    if (autoChannelSetWifi5G === true) {
      ts.setCompletedSuccessfulStatus();
      ts.setOkMessage();
    } else {
      ts.setCompletedWithErrorsStatus();
      ts.setSeverity('WARN');
      ts.setMessage("Auto channel not set");
      ts.addComments("Auto channel not selected for 5GHz", "There is a possibility of neighboring Wifi interference");
      ts.addActionTitle("Auto channel not selected.");
      ts.addActionDesc("If there are other wifi networks nearby, customer may have problems accessing the internet."
        + " Run Wifi survey panel to get more insights about interference in the channel used by Wifi");
      ts.addActionListItem(["Set wifi 5GHz channel to auto in acs"]);
    }
  }

  if (isWifi24GEnabled === 1 || isWifi24GEnabled === '1' || isWifi24GEnabled === true || isWifi24GEnabled === 'true') {
    var autochannelSetWifi24G = ts.checkAutoChannelSet(parameterValues, autoChannel24GParamName);
    if (autochannelSetWifi24G !== null &amp;&amp; autochannelSetWifi24G === true) {
      ts.setCompletedSuccessfulStatus();
      ts.setOkMessage();
    } else {
      ts.setCompletedWithErrorsStatus();
      ts.setSeverity('WARN');
      ts.setMessage("Auto channel not set");
      ts.addComments("Auto channel not selected for 2.4GHz", "There is a possibility of neighboring Wifi interference");
      if (ts.getActionTitle === null || ts.getActionTitle === 'undefined' || ts.getActionTitle === "") {
        ts.addActionTitle("Auto channel not selected.");
      }
      if (ts.getActionDesc === null || ts.getActionDesc === 'undefined' || ts.getActionDesc === "") {
        ts.addActionDesc("If there are other wifi networks nearby, customer may have problems accessing the internet."
          + " Run Wifi survey panel to get more insights about interference in the channel used by Wifi");
      }
      ts.addActionListItem(["Set wifi 2.4GHz channel to auto in acs"]);
    }
  }
  var resp = ts.returnTroubleshootingEventResponse();
  log.info(resp);
  publishMsg(resp);
}

function runUploadTest(isWifiEnabled, operations) {
  publishInProgressResponse(tests.uploadSpeedTest);
  log.info(isWifiEnabled);
  if (isWifiEnabled === false) {
    skipTest(isWifiEnabled);
    return;
  }
  var operationIds = ts.checkSpeedTestsAreComplete(operations);
  if (operationIds === null || (typeof operationIds.download) === 'undefined' || 0 === operations.length) {
    ts.setCompletedWithErrorsStatus();
    ts.setMessage("Test incomplete");
    ts.addComments("Unable to determine the upload speed", "There was a problem running upload speed test.");
    ts.addActionTitle("Unable to create device diagnostic operation");
    ts.addActionListItem(["Check if device is online", "Check if speed test diagnostics are set up in the device model"]);
  } else {
    var uploadSpeed = ts.getUploadSpeed(operationIds.upload);
    if (uploadSpeed &gt;= UPLOADSPEED_MIN_THRESHOLD_IN_MBPS) {
      ts.setCompletedSuccessfulStatus();
      ts.setOkMessage();
    } else {
      ts.setCompletedWithErrorsStatus();
      ts.setMessage("Low upload speed");
      ts.addComments("Upload speed is low", "Customer may have problems accessing the internet if the upload speed is low");
      ts.addActionTitle("Low upload speed");
      ts.addActionListItem(["UploadSpeed - " + uploadSpeed + "Mbps",
        "Open trouble ticket",
        "Confirm to the customer that when the problem is solved (approx. 1 day) we will notify them"]);
    }
  }
  var resp = ts.returnTroubleshootingEventResponse();
  log.info(resp);
  publishMsg(resp);
}

function runDownloadTest(isWifiEnabled, operations) {
  publishInProgressResponse(tests.downloadSpeedTest);
  log.info(isWifiEnabled);
  if (isWifiEnabled === false) {
    skipTest(isWifiEnabled);
    return;
  }
  var operationIds = ts.checkSpeedTestsAreComplete(operations);
  if (operationIds === null || (typeof operationIds.download) === 'undefined') {
    ts.setCompletedWithErrorsStatus();
    ts.setMessage("Test incomplete");
    ts.addComments("Unable to determine the download speed", "There was a problem running download speed test.");
    ts.addActionTitle("Unable to create device diagnostic operation");
    ts.addActionListItem(["Check if device is online", "Check if speed test diagnostics are set up in the device model"]);
  } else {
    var downloadSpeed = ts.getDownloadSpeed(operationIds.download);
    if (downloadSpeed &gt;= DOWNLOADSPEED_MIN_THRESHOLD_IN_MBPS) {
      ts.setCompletedSuccessfulStatus();
      ts.setOkMessage();
    } else {
      ts.setCompletedWithErrorsStatus();
      ts.setMessage("Low download speed");
      ts.addComments("Download speed is low", "Customer may have problems accessing the internet if the download speed is low");
      ts.addActionTitle("Low download speed");
      ts.addActionListItem(["DownloadSpeed - " + downloadSpeed + "Mbps",
        "Open trouble ticket",
        "Confirm to the customer that when the problem is solved (approx. 1 day) we will notify them"]);
    }
  }
  var resp = ts.returnTroubleshootingEventResponse();
  log.info(resp);
  publishMsg(resp);
}

function softwareVersionTest(isWifiEnabled) {
  publishInProgressResponse(tests.softwareVersionTest);
  if (isWifiEnabled === false) {
    skipTest(isWifiEnabled);
    return;
  }

  //Perform Test
  var firmwareUpgrade = ts.getFirmwareUpgrade();
  if (firmwareUpgrade !== null &amp;&amp; firmwareUpgrade !== 'undefined' &amp;&amp; firmwareUpgrade.length &gt; 0) {
    var upgradesAvailable = [];
    for (var i = 0; i &lt; firmwareUpgrade.length; i++) {
      upgradesAvailable.push(firmwareUpgrade[i].targetFirmware);
    }
    ts.setCompletedWithErrorsStatus();
    ts.setMessage("update available");
    ts.setSeverity("WARN");
    ts.addComments("Software version not latest", "The customer may experience problems if the software running in the device is outdated. Updating it to the latest available version is recommended.");
    ts.addActionTitle("Firmware Upgrade available - " + upgradesAvailable.join(" , "));
    ts.addActionListItem(["Trigger firmware upgrade in ACS"]);
  } else {
    ts.setCompletedSuccessfulStatus();
    ts.setMessage("Firmware is upto date");
  }

  var resp = ts.returnTroubleshootingEventResponse();
  log.info(resp);
  publishMsg(resp);
}

function connectedDevicesCount(isWifiEnabled) {
  publishInProgressResponse(tests.connectedDevicesCount);
  if (isWifiEnabled === false) {
    skipTest(isWifiEnabled);
    return;
  }

  //Perform Test
  var count = ts.getConnectedDevicesCount();
  if (count &gt;= 0 &amp;&amp; count &lt;= CONNECTEDDEVICES_MIN_THRESHOLD) {
    ts.setCompletedSuccessfulStatus();
    ts.setMessage(count);
  }

  if (count &gt; CONNECTEDDEVICES_MIN_THRESHOLD &amp;&amp; count &lt;= CONNECTEDDEVICES_MAX_THRESHOLD) {
    ts.setCompletedWithErrorsStatus();
    ts.setMessage(count);
    ts.setSeverity("WARN");
    ts.addComments("Connected Device may be high", "Confirm with the customer if the number is correct.");
    ts.addActionTitle("High Connected devices count");
    ts.addActionListItem(["Set Wifi security in ACS", "Check with customer and change password"]);
  }

  if (count &gt; CONNECTEDDEVICES_MAX_THRESHOLD) {
    ts.setCompletedWithErrorsStatus();
    ts.setMessage(count);
    ts.addComments("Connected Device too high", "There may be unauthorized devices connected to the Wifi network. Confirm with the customer if the number is correct or may be caused by intruders");
    ts.addActionTitle("High Connected devices count");
    ts.addActionListItem(["Set Wifi security in ACS", "Check with customer and change password"]);
  }

  var resp = ts.returnTroubleshootingEventResponse();
  log.info(resp);
  publishMsg(resp);
}

function getDefaultResponse(step) {
  ts.setStepId("Unknown test - " + step);
  ts.setCompletedWithErrorsStatus();
  ts.setMessage(errorMsg);
  ts.addPayloadToResponse();
  var resp = ts.returnTroubleshootingEventResponse();
  log.info(JSON.stringify(resp));
  publishMsg(resp);
}

function publishErrorResponse(errorMsg) {
  ts.setStepId("Unknown test");
  ts.setCompletedWithErrorsStatus();
  ts.setMessage(errorMsg);
  ts.addPayloadToResponse();
  var resp = ts.returnTroubleshootingEventResponse();
  log.info(JSON.stringify(resp));
  publishMsg(resp);
}

function startStep() {
  ts.setStepId("");
  ts.setInProgressStatus();
  ts.addPayloadToResponse();
}

function publishInProgressResponse(stepId) {
  sleep(3000);
  ts.clearActions();
  ts.clearComments();
  ts.setStepId(stepId);
  ts.setInProgressStatus();
  ts.setMessage("");
  ts.setSeverity("");
  var InProgressResponse = ts.returnTroubleshootingEventResponse();
  log.info(JSON.stringify(InProgressResponse));
  publishMsg(InProgressResponse);
}

function sleep(milliseconds) {
  var date = Date.now();
  var currentDate = null;
  do {
    currentDate = Date.now();
  } while (currentDate - date &lt; milliseconds);
}

function skipTest(isWifiEnabled) {
  if (isWifiEnabled === false) {
    ts.setCompletedWithErrorsStatus();
    ts.setMessage("Skipped");
    ts.addComments("Wifi not enabled", "Wifi should be enabled to proceed with the automated troubleshooting");
    ts.addActionTitle("Enable wifi 2.4GHz/5GHz");
    ts.addActionListItem(["Enable wifi in ACS", "Run the troubleshooter again after enabling the Wifi"]);
    var resp = ts.returnTroubleshootingEventResponse();
    log.info(resp);
    publishMsg(resp);
  }
}

var operationType = scriptParameters.operationType;
var deviceId = scriptParameters.deviceId;
var stepsToBeExecuted = scriptParameters.executionSteps;
var errorMsg;

if (!operationType) {
  errorMsg = 'Unable to execute script. operationType must be specified';
  publishErrorResponse(errorMsg);
}


var response = {};
switch (operationType) {
  case 'READ':
    response = {
      type: 'GuidedSteps',
      steps: [
        {
          id: tests.wifi24GTest,
          label: 'WiFi 2.4GHz',
          description: 'Is 2.4 GHz enabled?',
          selected: true
        },
        {
          id: tests.wifi5GTest,
          label: 'WiFi 5GHz',
          description: 'Is 5 GHz enabled?',
          selected: true
        },
        {
          id: tests.connectedDevicesCount,
          label: 'Connected Devices',
          description: 'WiFi speed test',
          selected: true
        },
        {
          id: tests.signalStrengthTest,
          label: 'WiFi signal strength',
          description: 'check connection status',
          selected: true
        },
        {
          id: tests.softwareVersionTest,
          label: 'Device Software Version',
          description: 'current firmware version',
          selected: true
        },
        {
          id: tests.uploadSpeedTest,
          label: 'Upload SpeedTest',
          description: 'WiFi speed test',
          selected: true
        },
        {
          id: tests.downloadSpeedTest,
          label: 'Download SpeedTest',
          description: 'WiFi speed test',
          selected: true
        },
        {
          id: tests.interferenceTest,
          label: 'WiFi Interference',
          description: 'Is there any wi-fi interference',
          selected: true
        }
      ]
    };
    break;

  case 'UPDATE':
    //if (!Array.isArray(scriptParameters.executionSteps)) {
    //   errorMsg = 'guided troubleshooting steps are not specified correctly. Expected Array but got ' + typeof scriptParameters.executionSteps;
    //   publishErrorResponse(errorMsg);
    //}
    var steps = [];
    if (stepsToBeExecuted === null || stepsToBeExecuted === undefined || stepsToBeExecuted === '[]') {
      steps = [tests.wifi24GTest,
      tests.wifi5GTest,
      tests.connectedDevicesCount,
      tests.signalStrengthTest,
      tests.softwareVersionTest,
      tests.uploadSpeedTest,
      tests.downloadSpeedTest,
      tests.interferenceTest];
    } else {
      log.info(stepsToBeExecuted);
      var jsonData = JSON.parse(stepsToBeExecuted);
      for (var j = 0; j &lt; jsonData.length; j++) {
        steps.push(jsonData[j].name);
      }
    }

    response = {
      "deviceId": deviceId,
      "operationType": operationType,
      "executionSteps": stepsToBeExecuted
    };

    var parameterValues = acs.getDeviceParametersFromRest({
      deviceId: scriptParameters.deviceId,
      names: testParameters
    });

    //Update cpeParameterName with the relevant parameter name
    var isWifi24GEnabled = ts.getWifiBand(parameterValues, wifi24GParamName);
    var isWifi5GEnabled = ts.getWifiBand(parameterValues, wifi5GParamName);
    log.info(isWifi24GEnabled + " " + isWifi5GEnabled);

    var isWifiEnabled = ((isWifi24GEnabled === 1 || isWifi24GEnabled === '1' || isWifi24GEnabled === true || isWifi24GEnabled === 'true') ||
      (isWifi5GEnabled === 1 || isWifi5GEnabled === '1' || isWifi5GEnabled === true || isWifi5GEnabled === 'true'));

    var operations = null;
    if (isWifiEnabled === true) {
      operations = ts.createSpeedTestOperation(deviceId, speedTestBody);
    }

    startStep();
    for (var i = 0; i &lt; steps.length; i++) {
      var step = steps[i];
      switch (step) {
        case tests.wifi24GTest:
          is24GEnabled(isWifi24GEnabled);
          break;
        case tests.wifi5GTest:
          is5GEnabled(isWifi5GEnabled);
          break;
        case tests.signalStrengthTest:
          signalStrengthTest(isWifiEnabled);
          break;
        case tests.interferenceTest:
          interferenceTest(parameterValues, isWifiEnabled, isWifi24GEnabled, isWifi5GEnabled);
          break;
        case tests.uploadSpeedTest:
          runUploadTest(isWifiEnabled, operations);
          break;
        case tests.downloadSpeedTest:
          runDownloadTest(isWifiEnabled, operations);
          break;
        case tests.connectedDevicesCount:
          connectedDevicesCount(isWifiEnabled);
          break;
        case tests.softwareVersionTest:
          softwareVersionTest(isWifiEnabled);
          break;
        //default:
        //  publishErrorResponse('invalid test name ' + step);
        //  break;
      }
    }
    break;
  default:
    break;
}

if (scriptParameters.operationType === 'UPDATE') {
  java.lang.Thread.sleep(1000);
}
response;</javaScriptCode>
            </scriptDefinition>
        </dashboardPanelScript>
        <dashboardPanelScript name="##dashboard.device_info.name##" scriptType="DASHBOARD_SCRIPT">
            <scriptDefinition name="Huawei  Vero:##dashboard.device_info.name##(1)(1)(1)" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
            "friendlyName": "Cluster ID",
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
            <scriptDefinition name="Huawei  Vero:##dashboard.tr069_config.name##(1)(1)(1)" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
                    <key>readonly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
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
                    <key>readonly</key>
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
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>readonly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">true</value>
                </entry>
                <entry>
                    <key>parameter</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">InternetGatewayDevice.DeviceInfo.UpTime</value>
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
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>readonly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">true</value>
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
                    <key>readonly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">TR-69 Config</value>
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
                    <key>readonly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WAN</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">17</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>readonly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">16</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>readonly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 5</value>
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
                    <key>readonly</key>
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
        <widgets name="Connected Devices" type="CONNECTED_DEVICES" description="Connected Devices" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">three-desktops</value>
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
                    <key>readonly</key>
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
                    <key>readonly</key>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">19</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>readonly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">DHCP</value>
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
                    <key>readonly</key>
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
                    <key>readonly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">23</value>
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
        <widgets name="Diagnostics" type="DIAGNOSTICS" description="Device Diagnostics" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">stethoscope</value>
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
                    <key>readonly</key>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">24</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>readonly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">true</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">Device Log</value>
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
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>readonly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">true</value>
                </entry>
                <entry>
                    <key>parameter</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">InternetGatewayDevice.WANDevice.1.WANCommonInterfaceConfig.TotalBytesSent</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">18</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
                <entry>
                    <key>readonly</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">false</value>
                </entry>
                <entry>
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 1</value>
                </entry>
            </configuration>
        </widgets>
        <allowAllGroups>TRUE</allowAllGroups>
        <config/>
    </dashboards>
    <dashboardPanels>
        <dashboardPanel name="Uptime" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"859b0655-7c79-d206-e647-0dcef75224de","panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/91cc5b80-ca22-11eb-898c-b150debb2799?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:0.5,filter:(language:kuery,query:''),formatter:'s,h,1',id:'61ca57f1-469d-11e7-af02-69e470af7417',label:Uptime,line_width:1,metrics:!((field:params.InternetGatewayDevice.DeviceInfo.UpTime,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries,value_template:'%7B%7Bvalue%7D%7D%20horas')),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Uptime%20-%20Per%20Device',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="WiFi 2.4" panelType="PANEL_DASHBOARD_SERVICE_CONFIG">
            <configuration>{"dataSource":{"type":"SERVICE_CONFIGURATION_SCRIPT","sourceId":"WiFi 1","sourceIdSet":[]},"readOnly":false,"tabName":"8dfb8f69-7436-21fa-2ff7-7d256e19ce83","panelSource":"PANEL_DASHBOARD_SERVICE_CONFIG","dataType":"SERVICE_CONFIGURATION_SCRIPT","dataSourceServiceConfig":"cc34e734-2bb3-6326-1f1a-5aa560b88810"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Wi-Fi Home Score" panelType="PANEL_DASHBOARD_WIFI_SCORE">
            <configuration>{"readOnly":false,"tabName":"d3137426-e14d-a4c1-f62c-e9f0c4d4d628","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_WIFI_SCORE"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.session_info.name##" panelType="PANEL_DASHBOARD_SESSION_INFO">
            <configuration>{"buttons":{"handlers":[{"text":"Initiate Session","handler":"initiateSession","endpoint":{"url":"/devices/{deviceId}/connectionrequest?async=true","verb":"POST"},"visible":true,"tab":null}]},"websockets":{"ws":"/devices/{deviceId}?X-Atmosphere-tracking-id=0&amp;X-Cache-Date=0&amp;Content-Type=application/json&amp;X-atmo-protocol=true","handlers":[{"type":"TR69_INFORM_EVENT"},{"type":"TR69_SESSION_EVENT"},{"type":"TR69_CONNECTION_REQUEST_EVENT"}]},"readOnly":false}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.sync_status.name##" panelType="PANEL_STATUS_SYNC">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.up_time.name##" panelType="PANEL_STATUS_UPTIME">
            <configuration>{"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.DeviceInfo.UpTime","sourceIdSet":[]},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"duration":{"enable":true,"unit":"seconds"}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Alerts" panelType="PANEL_STATUS_ALERTS">
            <configuration>{"rules":{"threshold":"NONE","ok":{"className":"ok"},"warning":{"className":"warning"},"failure":{"className":"failure"}},"category":"NUMERIC"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.admin_actions.name##" panelType="PANEL_DEVICE_OPERATIONS_ADMIN">
            <configuration>{"actionsConfig":[{"id":"ManageOperation","text":"Manage Operations","url":"#devices/{deviceId}/active-operations","order":1,"visible":true},{"id":"ObjectStructParameter","text":"Manage Object Structure &amp; Parameters","url":"#devices/{deviceId}/parameters","order":2,"visible":true},{"id":"ManageGroupings","text":"Manage Groupings","url":"#devices/{deviceId}/device-groups","order":3,"visible":true},{"id":"ViewDeviceInfo","text":"View Device Information","url":"#devices/{deviceId}/device","order":4,"visible":true},{"id":"DeviceWorkbench","text":"Device Workbench","url":"#devices/{deviceId}/workbench","order":5,"visible":true},{"id":"ComplianceTestSuite","text":"Run Compliance Test Suite","url":"#devices/{deviceId}/execute-device-compliance-suite","order":6,"visible":true},{"id":"PerformActions","text":"Perform Actions","url":"#devices/{deviceId}/devicemodel/{deviceModelId}/device_actions","order":7,"visible":true},{"id":"PerformDiagnostics","text":"Perform Diagnostics","url":"#devices/{deviceId}/devicemodel/{deviceModelId}/diagnostics","order":8,"visible":true}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.tr069_config.name##" panelType="PANEL_DASHBOARD_TR069_CONFIG">
            <configuration>{"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"##dashboard.tr069_config.name##","sourceIdSet":[]},"buttons":{"handlers":[{"text":"Save","handler":"saveServiceConfigParameters","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"POST"},"visible":true,"tab":null},{"text":"Cancel","handler":"cancel","endpoint":{"url":"/deviceoperations/cancellation","verb":"POST"},"visible":false,"tab":null},{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"readOnly":false}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Pacotes Descartados 2.4Ghz" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"8dfb8f69-7436-21fa-2ff7-7d256e19ce83","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/dd626ef0-9028-11ec-a070-35c390214c77?embed=true&amp;type=metrics&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:'rgba(96,146,192,1)',fill:'0',formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'Pacotes%20Enviados%20Descartado',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Stats.DiscardPacketsSent,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries),(axis_position:right,chart_type:line,color:'rgba(211,96,134,1)',fill:'0',formatter:number,id:'99664230-9028-11ec-8823-65b10961c04e',label:'Pacotes%20Recebidos%20Descartado',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Stats.DiscardPacketsReceived,id:'99664231-9028-11ec-8823-65b10961c04e',type:max)),point_size:1,separate_axis:0,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Pacotes%20Descartados%202.4%20Ghz',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Broadband speed test" panelType="PANEL_DASHBOARD_BROADBAND_SPEED">
            <configuration>{"diagnosticsConfig":[{"id":"Download Diagnostics","subType":"DOWNLOADSPEED","diagnosticParameters":[{"name":"InternetGatewayDevice.DownloadDiagnostics.DownloadURL","value":"http://35.215.210.14:9090/download.bin"},{"name":"InternetGatewayDevice.DownloadDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.DownloadDiagnostics.DSCP","value":""},{"name":"InternetGatewayDevice.DownloadDiagnostics.EthernetPriority","value":""}]},{"id":"Upload Diagnostics","subType":"UPLOADSPEED","diagnosticParameters":[{"name":"InternetGatewayDevice.UploadDiagnostics.EthernetPriority","value":""},{"name":"InternetGatewayDevice.UploadDiagnostics.UploadURL","value":"http://35.215.210.14:9090/upload.bin"},{"name":"InternetGatewayDevice.UploadDiagnostics.DSCP","value":""},{"name":"InternetGatewayDevice.UploadDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.UploadDiagnostics.TestFileLength","value":"1000"}]}],"tabName":"32e031f9-059c-180e-204f-cba31eea987b","InternetGatewayDevice.DownloadDiagnostics.DownloadURL":"http://35.215.210.14:9090/download.bin","InternetGatewayDevice.DownloadDiagnostics.Interface":"","InternetGatewayDevice.DownloadDiagnostics.DSCP":"","InternetGatewayDevice.DownloadDiagnostics.EthernetPriority":"","InternetGatewayDevice.UploadDiagnostics.EthernetPriority":"","InternetGatewayDevice.UploadDiagnostics.UploadURL":"http://35.215.210.14:9090/upload.bin","InternetGatewayDevice.UploadDiagnostics.DSCP":"","InternetGatewayDevice.UploadDiagnostics.Interface":"","InternetGatewayDevice.UploadDiagnostics.TestFileLength":"1000"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Power Volt." panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"units":"mv","rules":{"threshold":"NONE","ok":{"className":"ok"},"warning":{"className":"warning"},"failure":{"className":"failure"}},"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.WANDevice.1.X_GponInterafceConfig.SupplyVoltage"},"category":"NUMERIC"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Wan PPP" panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"rules":{"threshold":"NONE","ok":{"className":"ok"},"warning":{"className":"warning"},"failure":{"className":"failure"}},"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.WANDevice.1.WANConnectionDevice.3.WANPPPConnection.1.ConnectionStatus"},"category":"ENUM"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.device_actions.name##" panelType="PANEL_DEVICE_OPERATIONS_ACTIONS">
            <configuration>{"actionsConfig":[],"moreButton":{"handlers":[{"text":"##dashboard.more_device_actions##","handler":"showMoreActions","visible":true}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="TX" panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"units":"db","rules":{"threshold":"DECREASING","ok":{"className":"ok","message":"OK"},"warning":{"className":"warning","message":"Atenção","value":-25},"failure":{"className":"failure","message":"Critico","value":-27}},"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.WANDevice.1.X_GponInterafceConfig.TXPower"},"category":"NUMERIC"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Nível TX / RX" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"859b0655-7c79-d206-e647-0dcef75224de","panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/a6ec0270-8e8d-11eb-9808-f3ffb7f10f38?embed=true&amp;type=metrics&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:'rgba(214,191,87,1)',fill:'-3.4',formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:RX,line_width:1,metrics:!((field:params.InternetGatewayDevice.WANDevice.1.X_GponInterafceConfig.RXPower,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries),(axis_position:right,chart_type:line,color:'rgba(231,102,76,1)',fill:'0.0',formatter:number,id:'73e061f0-8e8d-11eb-a513-2709adbf6ad7',label:TX,line_width:1,metrics:!((field:params.InternetGatewayDevice.WANDevice.1.X_GponInterafceConfig.TXPower,id:'73e061f1-8e8d-11eb-a513-2709adbf6ad7',type:max)),point_size:1,separate_axis:0,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'RX%20%2FTX%20por%20dispositivo',type:metrics))","diagnosticsConfig":[{"diagnosticParameters":[]}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.broadband_speed_hist.name##" panelType="PANEL_DASHBOARD_BROADBAND_HISTORICAL">
            <configuration>{"buttons":{"handlers":[{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"tableConfig":{"searchName":"PANEL_DASHBOARD_BROADBAND_HISTORICAL","title":"Historic Broadband Speed Test Results","searchParams":{"tableName":"DIAGNOSTIC_RESULT_SUMMARY","url":"/devices/{deviceId}/diagnostics/speedtest","q":"PINGTESTDATE is null","pageSize":20,"orderBy":"LASTMODIFIED","ascending":false},"columns":[{"name":"time","field":"lastModified","label":"Time","align":"left","dataType":"DATETIME","fieldFormat":"hh:mma, dd MMM yyyy"},{"name":"dload","field":"downloadSpeed","label":"Download Speed (Mbps)","align":"center","dataType":"MBYTES","fieldFormat":"%.1f"},{"name":"uload","field":"uploadSpeed","label":"Upload Speed (Mbps)","align":"center","dataType":"MBYTES","fieldFormat":"%.1f"}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.failed_operations.name##" panelType="PANEL_STATUS_OPERATIONS_FAILED">
            <configuration>{"links":{"#panelStatusOperationsFailed":{"url":"#devices/{deviceId}/failed-operations"}},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"rules":{"type":"numeric","threshold":"NONE"},"unit":null}</configuration>
        </dashboardPanel>
        <dashboardPanel name="DHCP" panelType="PANEL_DASHBOARD_SERVICE_CONFIG">
            <configuration>{"dataSource":{"type":"SERVICE_CONFIGURATION_SCRIPT","sourceId":"DHCP","sourceIdSet":[]},"readOnly":false,"tabName":"18b8b003-a999-f473-5ced-4836beae9d45","panelSource":"PANEL_DASHBOARD_SERVICE_CONFIG","dataType":"SERVICE_CONFIGURATION_SCRIPT","dataSourceServiceConfig":"f0fde627-d1ac-2147-5035-eee1d2b51fb4"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Dispositivos Conectados" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"859b0655-7c79-d206-e647-0dcef75224de","panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/17c6b210-8e8e-11eb-9808-f3ffb7f10f38?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:'rgba(145,112,184,1)',fill:0.5,formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'Dispositivos%20Conectados',line_width:1,metrics:!((field:params.Device.Hosts.X_HostNumberOfEntriesActive,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Dispositivos%20Conectados%20-%20Individual',type:metrics))","diagnosticsConfig":[{"diagnosticParameters":[]}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="CPU" panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"units":"%","rules":{"threshold":"INCREASING","ok":{"className":"ok","message":"OK"},"warning":{"className":"warning","message":"Atenção","value":50},"failure":{"className":"failure","message":"Crítico","value":70}},"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.DeviceInfo.ProcessStatus.CPUUsage"},"category":"NUMERIC"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Automated Troubleshooting" panelType="PANEL_DASHBOARD_TROUBLESHOOTING">
            <configuration>{"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"Automated Troubleshooting","sourceIdSet":[]},"readOnly":false,"tabName":"2d50d6c0-1f9b-9067-532d-7a8f346d6b6a","panelSource":"PANEL_DASHBOARD_TROUBLESHOOTING","pixelHeight":""}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Utilização Canal 2.4Ghz" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"8dfb8f69-7436-21fa-2ff7-7d256e19ce83","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/6badf9c0-902b-11ec-a070-35c390214c77?embed=true&amp;type=metrics&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-48h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:'0.1',filter:(language:kuery,query:''),formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'',line_width:1,metrics:!((id:'61ca57f2-469d-11e7-af02-69e470af7417',type:count)),point_size:1,separate_axis:0,split_color_mode:kibana,split_filters:!((color:%2368BC00,filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%201'),id:c0235550-902a-11ec-8823-65b10961c04e,label:'Canal%201'),(color:'rgba(84,179,153,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%202'),id:c94521e0-902a-11ec-8823-65b10961c04e,label:'Canal%202'),(color:'rgba(211,96,134,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%203'),id:d3408590-902a-11ec-8823-65b10961c04e,label:'Canal%203'),(color:'rgba(145,112,184,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%204'),id:d7d269c0-902a-11ec-8823-65b10961c04e,label:'Canal%204'),(color:'rgba(202,142,174,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%205'),id:dd5341d0-902a-11ec-8823-65b10961c04e,label:'Canal%205'),(color:'rgba(214,191,87,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%206'),id:e0a727c0-902a-11ec-8823-65b10961c04e,label:'Canal%206'),(color:'rgba(185,168,136,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%207'),id:e76b5540-902a-11ec-8823-65b10961c04e,label:'Canal%207'),(color:'rgba(218,139,69,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%208'),id:ea256c30-902a-11ec-8823-65b10961c04e,label:'Canal%208'),(color:'rgba(170,101,86,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%209'),id:eda32140-902a-11ec-8823-65b10961c04e,label:'Canal%209'),(color:'rgba(231,102,76,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%2010'),id:f106bea0-902a-11ec-8823-65b10961c04e,label:'Canal%2010'),(color:'rgba(22,0,188,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%2011'),id:f3c1bff0-902a-11ec-8823-65b10961c04e,label:'Canal%2011')),split_mode:filters,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'',tooltip_mode:show_all,type:timeseries),title:'Channel%202.4%20-%20Per%20Device',type:metrics))\n"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="WiFi Survey" panelType="PANEL_DASHBOARD_WIFISURVEY">
            <configuration>{"tabName":"8dfb8f69-7436-21fa-2ff7-7d256e19ce83","panelSource":"PANEL_DASHBOARD_WIFISURVEY"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Utilização CPU" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"f1d35ca5-fc89-4b7a-e67f-6c062b7117ca","panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/3721cde0-8e8c-11eb-9808-f3ffb7f10f38?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:0.5,formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'CPU%20%25',line_width:1,metrics:!((field:params.InternetGatewayDevice.DeviceInfo.ProcessStatus.CPUUsage,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'CPU%20-%20Individual',type:metrics))\n","diagnosticsConfig":[{"diagnosticParameters":[]}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Temperatura" panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"units":"C","rules":{"threshold":"INCREASING","ok":{"className":"ok","message":"OK"},"warning":{"className":"warning","message":"Atenção","value":40},"failure":{"className":"failure","message":"Crítico","value":70}},"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.WANDevice.1.X_GponInterafceConfig.TransceiverTemperature"},"category":"NUMERIC"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.device_info.name##" panelType="PANEL_DASHBOARD_DEVICE_INFO">
            <configuration>{"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"##dashboard.device_info.name##","sourceIdSet":[]},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"panelType":"PANEL_STATUS_ONLINE"}}]},"buttons":{"handlers":[{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"readOnly":true}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.common_issues.name##" panelType="PANEL_DEVICE_OPERATIONS_ISSUES">
            <configuration>{"actionsConfig":[{"order":0,"include":true,"text":"Incognito Support","url":"https://support.incognito.com/"}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="MTU" panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"units":"","rules":{"threshold":"INTERVAL","ok":{"className":"ok","message":""},"warning":{"className":"warning","message":"","value":1492},"failure":{"className":"failure","message":"","value":1492}},"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.WANDevice.1.WANConnectionDevice.3.WANPPPConnection.1.CurrentMRUSize"},"category":"NUMERIC"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.online.name##" panelType="PANEL_STATUS_ONLINE">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Trace Route" panelType="PANEL_DASHBOARD_TRACEROUTE">
            <configuration>{"diagnosticsConfig":[{"id":"TraceRoute Diagnostics","subType":"TRACEROUTE","diagnosticParameters":[{"name":"InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount","value":""},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.Host","value":"8.8.8.8"},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.Timeout","value":""},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries","value":""},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize","value":""},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.DSCP","value":""}]}],"tabName":"18b8b003-a999-f473-5ced-4836beae9d45","InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount":"","InternetGatewayDevice.TraceRouteDiagnostics.Host":"8.8.8.8","InternetGatewayDevice.TraceRouteDiagnostics.Timeout":"","InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries":"","InternetGatewayDevice.TraceRouteDiagnostics.Interface":"","InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize":"","InternetGatewayDevice.TraceRouteDiagnostics.DSCP":""}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.connected_devices.name##" panelType="PANEL_STATUS_CONNECTED">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"rules":{"type":"numeric","threshold":"NONE"}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="IP Ping Test" panelType="PANEL_DASHBOARD_IPPING">
            <configuration>{"diagnosticsConfig":[{"id":"IP Ping Diagnostics","subType":"IPPING","diagnosticParameters":[{"name":"InternetGatewayDevice.IPPingDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.IPPingDiagnostics.Host","value":"8.8.8.8"},{"name":"InternetGatewayDevice.IPPingDiagnostics.DSCP","value":""},{"name":"InternetGatewayDevice.IPPingDiagnostics.DataBlockSize","value":""},{"name":"InternetGatewayDevice.IPPingDiagnostics.Timeout","value":""},{"name":"InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions","value":""}]}],"tabName":"18b8b003-a999-f473-5ced-4836beae9d45","InternetGatewayDevice.IPPingDiagnostics.Interface":"","InternetGatewayDevice.IPPingDiagnostics.Host":"8.8.8.8","InternetGatewayDevice.IPPingDiagnostics.DSCP":"","InternetGatewayDevice.IPPingDiagnostics.DataBlockSize":"","InternetGatewayDevice.IPPingDiagnostics.Timeout":"","InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions":""}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Tráfego 2.4 GHz" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"8dfb8f69-7436-21fa-2ff7-7d256e19ce83","panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/9d1669f0-adc0-11eb-96c5-d3c911c2d6fb?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_min:'0',axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:0.5,formatter:bytes,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'Bytes%20sent',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.TotalBytesSent,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max),(field:'61ca57f2-469d-11e7-af02-69e470af7417',id:'0ec7af60-a91f-11eb-9f07-b1343aa3e324',lag:'',type:serial_diff)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries),(axis_position:right,chart_type:line,color:'rgba(211,96,134,1)',fill:0.5,formatter:number,id:'975bd3b0-a91f-11eb-9f07-b1343aa3e324',label:'Bytes%20Received',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.TotalBytesReceived,id:'975bd3b1-a91f-11eb-9f07-b1343aa3e324',type:max),(field:'975bd3b1-a91f-11eb-9f07-b1343aa3e324',id:a8a26f30-a91f-11eb-9f07-b1343aa3e324,lag:'',type:serial_diff)),point_size:1,separate_axis:0,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Wlan%202.4%20GHz%20-%20Per%20Device',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Connected Devices Topology" panelType="PANEL_DASHBOARD_CONNECTED_DEVICES">
            <configuration>{"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"Connected Devices Topology","sourceIdSet":[]},"readOnly":false,"tabName":"98037e66-d811-5f8f-ad39-368578dbb5fd","diagnosticsConfig":[{"diagnosticParameters":[],"subType":"DEVICES"}],"panelSource":"PANEL_DASHBOARD_CONNECTED_DEVICES"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.last_seen.name##" panelType="PANEL_STATUS_LASTSEEN">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"duration":{"enable":false,"unit":null}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.active_operations.name##" panelType="PANEL_STATUS_OPERATIONS_ACTIVE">
            <configuration>{"links":{"#panelStatusOperationsActive":{"url":"#devices/{deviceId}/active-operations"}},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"rules":{"type":"numeric","threshold":"NONE"},"unit":null}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Subscriber Info" panelType="PANEL_DASHBOARD_SUBSCRIBER_INFO">
            <configuration>{"tabName":"32e031f9-059c-180e-204f-cba31eea987b","panelSource":"PANEL_DASHBOARD_SUBSCRIBER_INFO","showMap":true}</configuration>
        </dashboardPanel>
        <dashboardPanel name="RX" panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"units":"db","rules":{"threshold":"DECREASING","ok":{"className":"ok","message":"OK"},"warning":{"className":"warning","message":"Atenção","value":-25},"failure":{"className":"failure","message":"Crítico","value":-27}},"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.WANDevice.1.X_GponInterafceConfig.RXPower"},"category":"NUMERIC"}</configuration>
        </dashboardPanel>
    </dashboardPanels>
    <dashboardLayout>{"version":"1.2","children":[{"type":"COLUMN_LEFT","order":0,"hasPanelChildren":false,"children":[{"name":"##dashboard.layout.region.device_ident##","type":"REGION_DEVICE_IDENTIFIER","order":0,"hasPanelChildren":false,"children":[{"name":"PANEL_COMMON_DEVICE_IDENTIFIER","type":"PANEL_COMMON_DEVICE_IDENTIFIER","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.customer_ident##","type":"REGION_CUSTOMER_IDENTIIFIER","order":1,"hasPanelChildren":true,"children":[{"name":"PANEL_COMMON_CUSTOMER_IDENTIFIER","type":"PANEL_COMMON_CUSTOMER_IDENTIFIER","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.images##","type":"REGION_DEVICE_IMAGES","order":2,"hasPanelChildren":true,"children":[{"name":"PANEL_COMMON_DEVICE_IMAGES","type":"PANEL_COMMON_DEVICE_IMAGES","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.operations##","type":"REGION_DEVICE_OPERATIONS","order":3,"hasPanelChildren":true,"children":[{"name":"##dashboard.device_actions.name##","type":"PANEL_DEVICE_OPERATIONS_ACTIONS","order":0,"hasPanelChildren":false},{"name":"##dashboard.common_issues.name##","type":"PANEL_DEVICE_OPERATIONS_ISSUES","order":1,"hasPanelChildren":false},{"name":"##dashboard.admin_actions.name##","type":"PANEL_DEVICE_OPERATIONS_ADMIN","order":2,"hasPanelChildren":false}]}]},{"type":"COLUMN_RIGHT","order":1,"hasPanelChildren":false,"children":[{"name":"##dashboard.layout.region.status##","type":"REGION_STATUS","order":0,"hasPanelChildren":true,"children":[{"name":"##dashboard.online.name##","type":"PANEL_STATUS_ONLINE","order":0,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.sync_status.name##","type":"PANEL_STATUS_SYNC","order":1,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.connected_devices.name##","type":"PANEL_STATUS_CONNECTED","order":2,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.active_operations.name##","type":"PANEL_STATUS_OPERATIONS_ACTIVE","order":3,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.failed_operations.name##","type":"PANEL_STATUS_OPERATIONS_FAILED","order":4,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.last_seen.name##","type":"PANEL_STATUS_LASTSEEN","order":5,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.up_time.name##","type":"PANEL_STATUS_UPTIME","order":6,"hasPanelChildren":false,"visible":true},{"name":"TX","type":"PANEL_STATUS_CUSTOM","order":7,"hasPanelChildren":false,"visible":true,"category":"NUMERIC"},{"name":"RX","type":"PANEL_STATUS_CUSTOM","order":8,"hasPanelChildren":false,"visible":true,"category":"NUMERIC"},{"name":"Temperatura","type":"PANEL_STATUS_CUSTOM","order":9,"hasPanelChildren":false,"visible":true,"category":"NUMERIC"},{"name":"CPU","type":"PANEL_STATUS_CUSTOM","order":10,"hasPanelChildren":false,"visible":true,"category":"NUMERIC"},{"name":"MTU","type":"PANEL_STATUS_CUSTOM","order":11,"hasPanelChildren":false,"visible":true,"category":"NUMERIC"},{"name":"Wan PPP","type":"PANEL_STATUS_CUSTOM","order":12,"hasPanelChildren":false,"visible":true,"category":"ENUM"},{"name":"Power Volt.","type":"PANEL_STATUS_CUSTOM","order":13,"hasPanelChildren":false,"visible":true,"category":"NUMERIC"},{"name":"Alerts","type":"PANEL_STATUS_ALERTS","order":14,"hasPanelChildren":false,"visible":true}]},{"name":"##dashboard.layout.region.csr_call_log##","type":"REGION_CSR_CALL_INFO","order":1,"hasPanelChildren":true,"children":[{"name":"##dashboard.csr_call_info.name##","type":"PANEL_COMMON_CSR_CALL_INFO","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.dashboards##","type":"REGION_DASHBOARDS","order":2,"hasPanelChildren":false,"children":[{"name":"##dashboard.tab.overview##","type":"TAB_DASHBOARD","order":0,"hasPanelChildren":true,"visible":true,"children":[{"name":"##dashboard.device_info.name##","type":"PANEL_DASHBOARD_DEVICE_INFO","order":0,"hasPanelChildren":false,"visible":true,"size":{"h":1,"v":1}},{"name":"##dashboard.session_info.name##","type":"PANEL_DASHBOARD_SESSION_INFO","order":1,"hasPanelChildren":false,"visible":true,"size":{"h":1,"v":1}},{"name":"Broadband speed test","type":"PANEL_DASHBOARD_BROADBAND_SPEED","order":2,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"##dashboard.broadband_speed_hist.name##","type":"PANEL_DASHBOARD_BROADBAND_HISTORICAL","order":3,"hasPanelChildren":false,"visible":true,"size":{"h":1,"v":1}},{"name":"Subscriber Info","type":"PANEL_DASHBOARD_SUBSCRIBER_INFO","order":4,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":2,"v":1}}]},{"name":"##dashboard.tab.topology##","type":"TAB_DASHBOARD","order":1,"hasPanelChildren":true,"visible":false,"children":[{"name":"Connected Devices Topology","type":"PANEL_DASHBOARD_CONNECTED_DEVICES","order":0,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":2,"v":2}}]},{"name":"##dashboard.tab.diagnostics##","type":"TAB_DASHBOARD","order":2,"hasPanelChildren":true,"visible":false,"children":[{"name":"Trace Route","type":"PANEL_DASHBOARD_TRACEROUTE","order":0,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"IP Ping Test","type":"PANEL_DASHBOARD_IPPING","order":1,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"##dashboard.tr069_config.name##","type":"PANEL_DASHBOARD_TR069_CONFIG","order":2,"hasPanelChildren":false,"visible":true,"size":{"h":1,"v":1}},{"name":"DHCP","type":"PANEL_DASHBOARD_SERVICE_CONFIG","order":3,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}}]},{"name":"WIFI - Gerencia","type":"TAB_DASHBOARD","order":3,"hasPanelChildren":true,"visible":true,"children":[{"name":"WiFi 2.4","type":"PANEL_DASHBOARD_SERVICE_CONFIG","order":0,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"WiFi Survey","type":"PANEL_DASHBOARD_WIFISURVEY","order":1,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":2,"v":1}},{"name":"Tráfego 2.4 GHz","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":2,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":2,"v":1}},{"name":"Utilização Canal 2.4Ghz","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":3,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Pacotes Descartados 2.4Ghz","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":4,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}}]},{"name":"Troubleshooting","type":"TAB_DASHBOARD","order":4,"hasPanelChildren":true,"visible":true,"children":[{"name":"Automated Troubleshooting","type":"PANEL_DASHBOARD_TROUBLESHOOTING","order":0,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":2}}]},{"name":"Graficos","type":"TAB_DASHBOARD","order":5,"hasPanelChildren":true,"visible":true,"children":[{"name":"Uptime","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":0,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":2,"v":1}},{"name":"Utilização CPU","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":1,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Nível TX / RX","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":2,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Dispositivos Conectados","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":3,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}}]},{"name":"Home Score","type":"TAB_DASHBOARD","order":6,"hasPanelChildren":true,"visible":true,"children":[{"name":"Wi-Fi Home Score","type":"PANEL_DASHBOARD_WIFI_SCORE","order":0,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":2}}]}]}]}]}</dashboardLayout>
