# Incognito DX ACS Dashboard

## WiFi 5Ghz Configuration Panel
### Device Vendor: Nokia
### Product Class	G-1425G-A

## WiFi Panel javaScriptCode:

var dsc = require("deviceserviceconfiguration");

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
    if (typeof cpeParameters.password1 !== 'undefined' && cpeParameters.password1 !== null) {
      parameter.value = cpeParameters.password1.value;
    }
  } else {
    if (cpeParameters.BeaconType.value == "Basic") {
       parameter.value = null;
    } else {
       if (typeof cpeParameters.password !== 'undefined' && cpeParameters.password !== null) {
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
      { systemName:"b, g", friendlyName: "Mixed 11b & 11g" },
      { systemName:"n", friendlyName: "11n Only" },
      { systemName:"b-g-n", friendlyName: "Mixed 11b, 11g & 11n" }
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
         // if(value < 0 || value > 165)
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
              if(PasswordIndex < 1 && PasswordIndex > 4)
                throw "SecurityMode: Key index must be between 1 and 4";
              cpeParameters.passwordIndex.value = scriptParameters.passwordIndex;
              cpeParameters.passwordIndex.updated = true;
            } else {
              throw "SecurityMode(a):Key index must be between 1 and 4";
            }
            
            if (typeof scriptParameters.Password1 != 'undefined' && scriptParameters.Password1 != null) {
              if(scriptParameters.Password1.length !== 0 && scriptParameters.Password1.length != 13 && scriptParameters.Password1.length != 5)
                throw "Password1 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password1.value = scriptParameters.Password1;
              cpeParameters.Password1.updated = true;
            }
            if (typeof scriptParameters.Password2 != 'undefined' && scriptParameters.Password2 != null) {
              if(scriptParameters.Password2.length !== 0 && scriptParameters.Password2.length != 13 && scriptParameters.Password2.length != 5)
                throw "Password2 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password2.value = scriptParameters.Password2;
              cpeParameters.Password2.updated = true;
            }
            if (typeof scriptParameters.Password3 != 'undefined' && scriptParameters.Password3 != null) {
              if(scriptParameters.Password3.length !== 0 && scriptParameters.Password3.length != 13 && scriptParameters.Password3.length != 5)
                throw "Password3 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password3.value = scriptParameters.Password3;
              cpeParameters.Password3.updated = true;
            }
            if (typeof scriptParameters.Password4 != 'undefined' && scriptParameters.Password4 != null) {
              if(scriptParameters.Password4.length !== 0 && scriptParameters.Password4.length != 13 && scriptParameters.Password4.length != 5)
                throw "Password4 length invalid. Must be 5 (64bit) or 13 (128bit) ASCII characters";
              cpeParameters.Password4.value = scriptParameters.Password4;
              cpeParameters.Password4.updated = true;
            }
            */

            if(value == "WEP-Shared") {
              cpeParameters.BasicAuthenticationMode.value = "SharedAuthentication";
              cpeParameters.BasicAuthenticationMode.updated = true;
              if (typeof scriptParameters.password != 'undefined' && scriptParameters.password !== null) {
                if(scriptParameters.password.length !== 0 && scriptParameters.password.length != 10)
                  throw "Password length invalid. Must be 10 ASCII characters";
                cpeParameters.passwordIndex.value = PasswordIndex;
                cpeParameters.passwordIndex.updated = true;
                cpeParameters.password1.value = scriptParameters.password;
                cpeParameters.password1.updated = true;
              }
              else {
                if(typeof scriptParameters.passwordIndex != 'undefined') {
                  PasswordIndex = parseInt(scriptParameters.passwordIndex,10);
                  if(PasswordIndex < 1 && PasswordIndex > 4)
                    throw "SecurityMode: Key index must be between 1 and 4";
                  cpeParameters.passwordIndex.value = scriptParameters.passwordIndex;
                  cpeParameters.passwordIndex.updated = true;
        
                  if (typeof scriptParameters.password1 != 'undefined' && scriptParameters.password1 !== null) {
                    if(scriptParameters.password1.length !== 0 && scriptParameters.password1.length != 10) 
                      throw "Password length invalid. Must be 10 ASCII characters";
                    cpeParameters.password1.value = scriptParameters.password1;
                    cpeParameters.password1.updated = true;
                  }
                } 
              }
            } else {
              cpeParameters.BasicAuthenticationMode.value = "None";
              cpeParameters.BasicAuthenticationMode.updated = true;
              if (typeof scriptParameters.password != 'undefined' && scriptParameters.password !== null) {
                if(scriptParameters.password.length !== 0 && scriptParameters.password.length != 13)
                  throw "Password length invalid. Must be 13 ASCII characters";
                cpeParameters.passwordIndex.value = PasswordIndex;
                cpeParameters.passwordIndex.updated = true;
                cpeParameters.password1.value = scriptParameters.password;
                cpeParameters.password1.updated = true;
              }
              else {
                if(typeof scriptParameters.passwordIndex != 'undefined') {
                  PasswordIndex = parseInt(scriptParameters.passwordIndex,10);
                  if(PasswordIndex < 1 && PasswordIndex > 4)
                    throw "SecurityMode: Key index must be between 1 and 4";
                  cpeParameters.passwordIndex.value = scriptParameters.passwordIndex;
                  cpeParameters.passwordIndex.updated = true;
        
                  if (typeof scriptParameters.password1 != 'undefined' && scriptParameters.password1 !== null) {
                    if(scriptParameters.password1.length !== 0 && scriptParameters.password1.length != 13)
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
            
            if (typeof scriptParameters.password != 'undefined' && scriptParameters.password !== null) {
              if(scriptParameters.password.length < 8)
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

            if (typeof scriptParameters.password != 'undefined' && scriptParameters.password !== null) {
              if(scriptParameters.password.length < 8)
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


response;

## DataModel in XML

<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<DeviceModel name="Nokia-ALCL-CaboNatal" manufacturer="Nokia-ALCL-CaboNatal" oui="184593,6CC63B,9075BC,E01FED,104738,549F06" productClass="G-2425G-A,G-140W-H,G-240W-G,G-1425G-A" objectModelDefinitions="InternetGatewayDevice:1.14 VoiceService:2.0 StorageService:1.2" description="" setNotification="true" setAccessList="true" protocolType="TR069">
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
    <supportedRPCMethods>ChangeDUState</supportedRPCMethods>
    <supportedRPCMethods>SetParameterValues</supportedRPCMethods>
    <supportedRPCMethods>Download</supportedRPCMethods>
    <supportedRPCMethods>FactoryReset</supportedRPCMethods>
    <options dashboardDevicePollTime="10" reloadOnFactoryReset="NEVER" collectConnectedDevices="false" addObjectBackfill="true" discoveryRetry="0" simpleDiscoveryRetry="3" simpleDiscoveryEnabled="false"/>
    <deviceServiceConfigurations name="WiFi 1">
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: WiFi 1" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="WAN 1">
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: WAN 1" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: WiFi 2" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: DHCP" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="WiFi 5">
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: WiFi 5" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
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
    <deviceServiceConfigurations name="WAN 4">
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: WAN 4" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="WAN 3">
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: WAN 3" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="Device Log">
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: Device Log" purpose="Device service configuration" tags="null" scriptParameters="[]">
            <javaScriptCode>var dsc = require("deviceserviceconfiguration");

var deviceId = scriptParameters.deviceId;
var response = dsc.getDeviceParameterLogs(deviceId);

response;
</javaScriptCode>
        </scriptDefinition>
    </deviceServiceConfigurations>
    <deviceServiceConfigurations name="WiFi 7">
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: WiFi 7" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: WiFi 6" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="WAN 2">
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: WAN 2" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="WiFi 8">
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: WiFi 8" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: WiFi 3" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceServiceConfigurations name="WiFi 4">
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: WiFi 4" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: TR-69 Config" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
    <deviceLogParameters name="Device Log 1" parameterName="InternetGatewayDevice.DeviceInfo.DeviceLog"/>
    <dataComposers name="Bytes Sent">
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: Bytes Sent" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
        <scriptDefinition name="Nokia-G-2425G-CaboNatal:Memoria Livre" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
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
        <scriptDefinition name="ALCL-G-2425G-CaboNatal: Bytes Received" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
        <dashboardPanelScript name="##dashboard.tr069_config.name##" scriptType="DASHBOARD_SCRIPT">
            <scriptDefinition name="ALCL-G-2425G-CaboNatal:##dashboard.tr069_config.name##" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
            <scriptDefinition name="ALCL-G-2425G-CaboNatal:##dashboard.connected_devices_topology.name##" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
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
        <dashboardPanelScript name="##dashboard.device_info.name##" scriptType="DASHBOARD_SCRIPT">
            <scriptDefinition name="ALCL-G-2425G-CaboNatal:##dashboard.device_info.name##" purpose="Device service configuration" tags="null" scriptParameters="[]">
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
        <dashboardPanelScript name="Automated Troubleshooting" scriptType="DASHBOARD_SCRIPT">
            <scriptDefinition name="Nokia-G-2425G-CaboNatal:Automated Troubleshooting" tags="null" scriptParameters="[{&quot;type&quot;:&quot;text&quot;}]">
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
          value: "http://192.168.252.2:9191/download.bin"
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
          value: "http://192.168.252.2:9191/upload.bin"
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">20</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">30</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">31</value>
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
        <widgets name="WiFi 6" type="SERVICE_CONFIGURATION" description="Wireless Network" stale="true">
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 6</value>
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
        <widgets name="Connected Devices" type="CONNECTED_DEVICES" description="Connected Devices" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">three-desktops</value>
                </entry>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">29</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">32</value>
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
        <widgets name="WiFi 5" type="SERVICE_CONFIGURATION" description="Wireless Network" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">wifi-signal</value>
                </entry>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 5</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">26</value>
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
        <widgets name="WAN 3" type="SERVICE_CONFIGURATION" description="Wide Area Network" stale="true">
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WAN 3</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">25</value>
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
        <widgets name="WiFi 7" type="SERVICE_CONFIGURATION" description="Wireless Network" stale="true">
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 7</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="WAN 1" type="SERVICE_CONFIGURATION" description="Wide Area Network" stale="true">
            <configuration>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WAN 1</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="WAN 4" type="SERVICE_CONFIGURATION" description="Wide Area Network" stale="true">
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WAN 4</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="WAN 2" type="SERVICE_CONFIGURATION" description="Wide Area Network" stale="true">
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WAN 2</value>
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
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">19</value>
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
        <widgets name="WiFi 3" type="SERVICE_CONFIGURATION" description="Wireless Network" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">wifi-signal</value>
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
                    <key>service</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">WiFi 3</value>
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
        <widgets name="Diagnostics" type="DIAGNOSTICS" description="Device Diagnostics" stale="true">
            <configuration>
                <entry>
                    <key>icon</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">stethoscope</value>
                </entry>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">28</value>
                </entry>
                <entry>
                    <key>size</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">size-1x1</value>
                </entry>
            </configuration>
        </widgets>
        <widgets name="DHCP" type="SERVICE_CONFIGURATION" description="Device DHCP" stale="true">
            <configuration>
                <entry>
                    <key>index</key>
                    <value xsi:type="xs:string" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">27</value>
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
        <allowAllGroups>TRUE</allowAllGroups>
        <config/>
    </dashboards>
    <dashboardPanels>
        <dashboardPanel name="Memória" panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"units":"kb","rules":{"threshold":"NONE","ok":{"className":"ok"},"warning":{"className":"warning"},"failure":{"className":"failure"}},"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.DeviceInfo.MemoryStatus.Free"},"category":"NUMERIC","limits":{}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Memória Livre" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"7126f81f-501a-6888-c433-01e57632d3b3","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/eab2dc00-d5d6-11eb-898c-b150debb2799?embed=true&amp;type=metrics&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:0.5,formatter:bytes,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'Memoria%20Livre',line_width:1,metrics:!((field:params.InternetGatewayDevice.DeviceInfo.MemoryStatus.Free,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Memory%20free%20-%20Per%20Device',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Utilização Canal 5Ghz" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"5b081482-64dc-c72e-3ac8-f63479624e51","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/2872d820-bb22-11ec-96e0-c516b8f93291?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'1m',isModelInvalid:!f,series:!((axis_position:right,chart_type:bar,color:%2368BC00,fill:'1',filter:(language:kuery,query:''),formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'',line_width:'6',metrics:!((id:'61ca57f2-469d-11e7-af02-69e470af7417',type:count)),point_size:1,separate_axis:0,split_color_mode:kibana,split_filters:!((color:%2368BC00,filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2036'),id:c0235550-902a-11ec-8823-65b10961c04e,label:'Canal%2036'),(color:'rgba(84,179,153,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel:%2040'),id:c94521e0-902a-11ec-8823-65b10961c04e,label:'Canal%2040'),(color:'rgba(211,96,134,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2044'),id:d3408590-902a-11ec-8823-65b10961c04e,label:'Channel%2044'),(color:'rgba(145,112,184,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2048'),id:d7d269c0-902a-11ec-8823-65b10961c04e,label:'Channel%2048'),(color:'rgba(202,142,174,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2052'),id:dd5341d0-902a-11ec-8823-65b10961c04e,label:'Channel%2052'),(color:'rgba(214,191,87,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2056'),id:e0a727c0-902a-11ec-8823-65b10961c04e,label:'Channel%2056'),(color:'rgba(185,168,136,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2060'),id:e76b5540-902a-11ec-8823-65b10961c04e,label:'Channel%2060'),(color:'rgba(218,139,69,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2064'),id:ea256c30-902a-11ec-8823-65b10961c04e,label:'Channel%2064'),(color:'rgba(170,101,86,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20100'),id:eda32140-902a-11ec-8823-65b10961c04e,label:'Channel%20100'),(color:'rgba(231,102,76,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20104'),id:f106bea0-902a-11ec-8823-65b10961c04e,label:'Channel%20104'),(color:'rgba(22,0,188,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20108'),id:f3c1bff0-902a-11ec-8823-65b10961c04e,label:'Channel%20108'),(color:'rgba(231,240,129,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20112'),id:cce01c50-90c1-11ec-8419-030540e36e5c,label:'Channel%20112'),(color:'rgba(115,232,113,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20116'),id:d16667c0-90c1-11ec-8419-030540e36e5c,label:'Channel%20116'),(color:'rgba(130,80,107,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20120'),id:d4d3c920-90c1-11ec-8419-030540e36e5c,label:'Channel%20120'),(color:'rgba(247,112,112,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel:%20124'),id:dd5c62f0-90c1-11ec-8419-030540e36e5c,label:'Channel%20124'),(color:'rgba(1,120,66,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20128'),id:e29387d0-90c1-11ec-8419-030540e36e5c,label:'Channel%20128'),(color:'rgba(235,198,97,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20132'),id:e7a6f810-90c1-11ec-8419-030540e36e5c,label:'Channel%20132'),(color:'rgba(205,98,139,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20136'),id:ed97f710-90c1-11ec-8419-030540e36e5c,label:'Channel%20136'),(color:'rgba(50,62,122,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20140'),id:f3d2a940-90c1-11ec-8419-030540e36e5c,label:'Channel%20140'),(color:'rgba(41,105,128,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20144'),id:f5baa320-90c1-11ec-8419-030540e36e5c,label:'Channel%20144'),(color:'rgba(38,67,83,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20149'),id:f9f3e000-90c1-11ec-8419-030540e36e5c,label:'Channel%20149'),(color:'rgba(96,125,61,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20153'),id:'518470a0-b4e4-11ec-8956-e556ebb5a566',label:'Channel%20153'),(color:'rgba(246,151,182,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20157'),id:'64c814a0-b4e4-11ec-8956-e556ebb5a566',label:'Channel%20157'),(color:'rgba(236,205,177,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel:%20161'),id:'7047f570-b4e4-11ec-8956-e556ebb5a566',label:'Channel%20161')),split_mode:filters,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Channel%205Ghz%20Geral%20-%20Per%20Device',type:metrics))\n"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Níveis TX/RX" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"7126f81f-501a-6888-c433-01e57632d3b3","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/18974960-b503-11ec-972b-717da09fcff7?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-7d,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:'rgba(214,191,87,1)',fill:'-3.4',formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:RX,line_width:1,metrics:!((field:params.InternetGatewayDevice.X_ALU_OntOpticalParam.TXPower,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries),(axis_position:right,chart_type:line,color:'rgba(231,102,76,1)',fill:'0.0',formatter:number,id:'73e061f0-8e8d-11eb-a513-2709adbf6ad7',label:TX,line_width:1,metrics:!((field:params.InternetGatewayDevice.X_ALU_OntOpticalParam.RXPower,id:'73e061f1-8e8d-11eb-a513-2709adbf6ad7',type:max)),point_size:1,separate_axis:0,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'RX%20%2FTX%20por%20dispositivo%20-%20Nokia',type:metrics))\n"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.device_actions.name##" panelType="PANEL_DEVICE_OPERATIONS_ACTIONS">
            <configuration>{"actionsConfig":[{"id":"Reboot","order":0,"visible":true},{"id":"Reload","order":2,"visible":true},{"id":"ReloadDataModel","order":1,"visible":true}],"moreButton":{"handlers":[{"text":"##dashboard.more_device_actions##","handler":"showMoreActions","visible":false}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="WiFi 2.4Ghz" panelType="PANEL_DASHBOARD_SERVICE_CONFIG">
            <configuration>{"readOnly":false,"tabName":"5b081482-64dc-c72e-3ac8-f63479624e51","dataSource":{"type":"SERVICE_CONFIGURATION_SCRIPT","sourceId":"WiFi 1","sourceIdSet":[]},"diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_SERVICE_CONFIG","dataType":"SERVICE_CONFIGURATION_SCRIPT","dataSourceServiceConfig":"dff1a381-3752-9744-ce76-aae02a6051eb"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.session_info.name##" panelType="PANEL_DASHBOARD_SESSION_INFO">
            <configuration>{"buttons":{"handlers":[{"text":"Initiate Session","handler":"initiateSession","endpoint":{"url":"/devices/{deviceId}/connectionrequest?async=true","verb":"POST"},"visible":true,"tab":null}]},"websockets":{"ws":"/devices/{deviceId}?X-Atmosphere-tracking-id=0&amp;X-Cache-Date=0&amp;Content-Type=application/json&amp;X-atmo-protocol=true","handlers":[{"type":"TR69_INFORM_EVENT"},{"type":"TR69_SESSION_EVENT"},{"type":"TR69_CONNECTION_REQUEST_EVENT"}]},"readOnly":false}</configuration>
        </dashboardPanel>
        <dashboardPanel name="WiFi Tráfego 5Ghz" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"5b081482-64dc-c72e-3ac8-f63479624e51","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/e04a2760-af51-11eb-b4c0-318651a5d1eb?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_min:'0',axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:0.5,formatter:bytes,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'Bytes%20sent',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.TotalBytesSent,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max),(field:'61ca57f2-469d-11e7-af02-69e470af7417',id:'0ec7af60-a91f-11eb-9f07-b1343aa3e324',lag:'',type:serial_diff)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries),(axis_position:right,chart_type:line,color:'rgba(211,96,134,1)',fill:0.5,formatter:number,id:'975bd3b0-a91f-11eb-9f07-b1343aa3e324',label:'Bytes%20Received',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.TotalBytesReceived,id:'975bd3b1-a91f-11eb-9f07-b1343aa3e324',type:max),(field:'975bd3b1-a91f-11eb-9f07-b1343aa3e324',id:a8a26f30-a91f-11eb-9f07-b1343aa3e324,lag:'',type:serial_diff)),point_size:1,separate_axis:0,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Wlan%205GHz%20-%20Per%20Device',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Uptime" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"7126f81f-501a-6888-c433-01e57632d3b3","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/91cc5b80-ca22-11eb-898c-b150debb2799?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:0.5,filter:(language:kuery,query:''),formatter:'s,h,1',id:'61ca57f1-469d-11e7-af02-69e470af7417',label:Uptime,line_width:1,metrics:!((field:params.InternetGatewayDevice.DeviceInfo.UpTime,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries,value_template:'%7B%7Bvalue%7D%7D%20horas')),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Uptime%20-%20Per%20Device',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.active_operations.name##" panelType="PANEL_STATUS_OPERATIONS_ACTIVE">
            <configuration>{"links":{"#panelStatusOperationsActive":{"url":"#devices/{deviceId}/active-operations"}},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"rules":{"type":"numeric","threshold":"NONE"},"unit":null}</configuration>
        </dashboardPanel>
        <dashboardPanel name="IP Ping Test" panelType="PANEL_DASHBOARD_IPPING">
            <configuration>{"diagnosticsConfig":[{"id":"IP Ping Diagnostics","subType":"IPPING","diagnosticParameters":[{"name":"InternetGatewayDevice.IPPingDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.IPPingDiagnostics.Host","value":"8.8.8.8"},{"name":"InternetGatewayDevice.IPPingDiagnostics.DSCP","value":""},{"name":"InternetGatewayDevice.IPPingDiagnostics.DataBlockSize","value":"1000"},{"name":"InternetGatewayDevice.IPPingDiagnostics.Timeout","value":""},{"name":"InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions","value":""}]}],"tabName":"28c536f9-1ab6-e371-4e31-50252070d95b","InternetGatewayDevice.IPPingDiagnostics.Interface":"","InternetGatewayDevice.IPPingDiagnostics.Host":"8.8.8.8","InternetGatewayDevice.IPPingDiagnostics.DSCP":"","InternetGatewayDevice.IPPingDiagnostics.DataBlockSize":"1000","InternetGatewayDevice.IPPingDiagnostics.Timeout":"","InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions":""}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.sync_status.name##" panelType="PANEL_STATUS_SYNC">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.common_issues.name##" panelType="PANEL_DEVICE_OPERATIONS_ISSUES">
            <configuration>{"actionsConfig":[{"order":0,"include":true,"text":"Incognito Support","url":"https://support.incognito.com/"}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="WAN Connection" panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"rules":{"threshold":"NONE","ok":{"className":"ok"},"warning":{"className":"warning"},"failure":{"className":"failure"}},"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.WANDevice.1.WANConnectionDevice.1.WANIPConnection.1.ConnectionStatus"},"category":"ENUM","limits":{}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Pacotes Descartados 5Ghz" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"5b081482-64dc-c72e-3ac8-f63479624e51","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/6528bbf0-9029-11ec-a070-35c390214c77?embed=true&amp;type=metrics&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:'rgba(96,146,192,1)',fill:'0',formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'Pacotes%20Enviados%20Descartado',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Stats.DiscardPacketsSent,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries),(axis_position:right,chart_type:line,color:'rgba(211,96,134,1)',fill:'0',formatter:number,id:'99664230-9028-11ec-8823-65b10961c04e',label:'Pacotes%20Recebidos%20Descartado',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Stats.DiscardPacketsReceived,id:'99664231-9028-11ec-8823-65b10961c04e',type:max)),point_size:1,separate_axis:0,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Pacotes%20Descartados%205%20Ghz',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Tráfego 2.4Ghz" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"5b081482-64dc-c72e-3ac8-f63479624e51","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/2872d820-bb22-11ec-96e0-c516b8f93291?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'1m',isModelInvalid:!f,series:!((axis_position:right,chart_type:bar,color:%2368BC00,fill:'1',filter:(language:kuery,query:''),formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'',line_width:'6',metrics:!((id:'61ca57f2-469d-11e7-af02-69e470af7417',type:count)),point_size:1,separate_axis:0,split_color_mode:kibana,split_filters:!((color:%2368BC00,filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2036'),id:c0235550-902a-11ec-8823-65b10961c04e,label:'Canal%2036'),(color:'rgba(84,179,153,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel:%2040'),id:c94521e0-902a-11ec-8823-65b10961c04e,label:'Canal%2040'),(color:'rgba(211,96,134,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2044'),id:d3408590-902a-11ec-8823-65b10961c04e,label:'Channel%2044'),(color:'rgba(145,112,184,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2048'),id:d7d269c0-902a-11ec-8823-65b10961c04e,label:'Channel%2048'),(color:'rgba(202,142,174,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2052'),id:dd5341d0-902a-11ec-8823-65b10961c04e,label:'Channel%2052'),(color:'rgba(214,191,87,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2056'),id:e0a727c0-902a-11ec-8823-65b10961c04e,label:'Channel%2056'),(color:'rgba(185,168,136,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2060'),id:e76b5540-902a-11ec-8823-65b10961c04e,label:'Channel%2060'),(color:'rgba(218,139,69,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%2064'),id:ea256c30-902a-11ec-8823-65b10961c04e,label:'Channel%2064'),(color:'rgba(170,101,86,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20100'),id:eda32140-902a-11ec-8823-65b10961c04e,label:'Channel%20100'),(color:'rgba(231,102,76,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20104'),id:f106bea0-902a-11ec-8823-65b10961c04e,label:'Channel%20104'),(color:'rgba(22,0,188,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20108'),id:f3c1bff0-902a-11ec-8823-65b10961c04e,label:'Channel%20108'),(color:'rgba(231,240,129,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20112'),id:cce01c50-90c1-11ec-8419-030540e36e5c,label:'Channel%20112'),(color:'rgba(115,232,113,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20116'),id:d16667c0-90c1-11ec-8419-030540e36e5c,label:'Channel%20116'),(color:'rgba(130,80,107,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20120'),id:d4d3c920-90c1-11ec-8419-030540e36e5c,label:'Channel%20120'),(color:'rgba(247,112,112,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel:%20124'),id:dd5c62f0-90c1-11ec-8419-030540e36e5c,label:'Channel%20124'),(color:'rgba(1,120,66,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20128'),id:e29387d0-90c1-11ec-8419-030540e36e5c,label:'Channel%20128'),(color:'rgba(235,198,97,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20132'),id:e7a6f810-90c1-11ec-8419-030540e36e5c,label:'Channel%20132'),(color:'rgba(205,98,139,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20136'),id:ed97f710-90c1-11ec-8419-030540e36e5c,label:'Channel%20136'),(color:'rgba(50,62,122,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20140'),id:f3d2a940-90c1-11ec-8419-030540e36e5c,label:'Channel%20140'),(color:'rgba(41,105,128,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20144'),id:f5baa320-90c1-11ec-8419-030540e36e5c,label:'Channel%20144'),(color:'rgba(38,67,83,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20149'),id:f9f3e000-90c1-11ec-8419-030540e36e5c,label:'Channel%20149'),(color:'rgba(96,125,61,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20153'),id:'518470a0-b4e4-11ec-8956-e556ebb5a566',label:'Channel%20153'),(color:'rgba(246,151,182,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel%20:%20157'),id:'64c814a0-b4e4-11ec-8956-e556ebb5a566',label:'Channel%20157'),(color:'rgba(236,205,177,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel:%20161'),id:'7047f570-b4e4-11ec-8956-e556ebb5a566',label:'Channel%20161')),split_mode:filters,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Channel%205Ghz%20Geral%20-%20Per%20Device',type:metrics))\n"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Trace Route" panelType="PANEL_DASHBOARD_TRACEROUTE">
            <configuration>{"diagnosticsConfig":[{"id":"TraceRoute Diagnostics","subType":"TRACEROUTE","diagnosticParameters":[{"name":"InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount","value":""},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.Host","value":"8.8.8.8"},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.Timeout","value":""},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries","value":""},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize","value":""},{"name":"InternetGatewayDevice.TraceRouteDiagnostics.DSCP","value":""}]}],"tabName":"28c536f9-1ab6-e371-4e31-50252070d95b","InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount":"","InternetGatewayDevice.TraceRouteDiagnostics.Host":"8.8.8.8","InternetGatewayDevice.TraceRouteDiagnostics.Timeout":"","InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries":"","InternetGatewayDevice.TraceRouteDiagnostics.Interface":"","InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize":"","InternetGatewayDevice.TraceRouteDiagnostics.DSCP":""}</configuration>
        </dashboardPanel>
        <dashboardPanel name="RX" panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"units":"db","rules":{"threshold":"DECREASING","ok":{"className":"ok","message":"OK"},"warning":{"className":"warning","message":"Atenção","value":-29},"failure":{"className":"failure","message":"Critico","value":-27}},"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.X_ALU_OntOpticalParam.RXPower"},"category":"NUMERIC","limits":{}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Pacotes Descartados 2.4Ghz" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"5b081482-64dc-c72e-3ac8-f63479624e51","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/dd626ef0-9028-11ec-a070-35c390214c77?embed=true&amp;type=metrics&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'15m',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:'rgba(96,146,192,1)',fill:'0',formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'Pacotes%20Enviados%20Descartado',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Stats.DiscardPacketsSent,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries),(axis_position:right,chart_type:line,color:'rgba(211,96,134,1)',fill:'0',formatter:number,id:'99664230-9028-11ec-8823-65b10961c04e',label:'Pacotes%20Recebidos%20Descartado',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Stats.DiscardPacketsReceived,id:'99664231-9028-11ec-8823-65b10961c04e',type:max)),point_size:1,separate_axis:0,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Pacotes%20Descartados%202.4%20Ghz',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="MTU" panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"units":"","rules":{"threshold":"INTERVAL","ok":{"className":"ok","message":"OK"},"warning":{"className":"warning","message":"Atenção","value":[1490,1495]},"failure":{"className":"failure","message":"Critico","value":[1489,1496]}},"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.WANDevice.1.WANConnectionDevice.1.WANIPConnection.1.MaxMTUSize"},"category":"NUMERIC","limits":{}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="CPU %" panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"units":"%","rules":{"threshold":"INCREASING","ok":{"className":"ok","message":"OK"},"warning":{"className":"warning","message":"Atenção","value":50},"failure":{"className":"failure","message":"Crítico","value":70}},"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.DeviceInfo.ProcessStatus.CPUUsage"},"category":"NUMERIC","limits":{}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.online.name##" panelType="PANEL_STATUS_ONLINE">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.failed_operations.name##" panelType="PANEL_STATUS_OPERATIONS_FAILED">
            <configuration>{"links":{"#panelStatusOperationsFailed":{"url":"#devices/{deviceId}/failed-operations"}},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"rules":{"type":"numeric","threshold":"NONE"},"unit":null}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Utilização CPU" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"7126f81f-501a-6888-c433-01e57632d3b3","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/3721cde0-8e8c-11eb-9808-f3ffb7f10f38?embed=true&amp;type=metrics&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-24h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:0.5,formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'CPU%20%25',line_width:1,metrics:!((field:params.InternetGatewayDevice.DeviceInfo.ProcessStatus.CPUUsage,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'CPU%20-%20Individual',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Temperatura" panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"units":"C","rules":{"threshold":"INCREASING","ok":{"className":"ok","message":"OK"},"warning":{"className":"warning","message":"Atenção","value":70},"failure":{"className":"failure","message":"Crítico","value":70}},"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.DeviceInfo.TemperatureStatus.TemperatureSensor.1.Value"},"category":"NUMERIC","limits":{}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.admin_actions.name##" panelType="PANEL_DEVICE_OPERATIONS_ADMIN">
            <configuration>{"actionsConfig":[{"id":"ManageOperation","text":"Manage Operations","url":"#devices/{deviceId}/active-operations","order":1,"visible":true},{"id":"ObjectStructParameter","text":"Manage Object Structure &amp; Parameters","url":"#devices/{deviceId}/parameters","order":2,"visible":true},{"id":"ManageGroupings","text":"Manage Groupings","url":"#devices/{deviceId}/device-groups","order":3,"visible":true},{"id":"ViewDeviceInfo","text":"View Device Information","url":"#devices/{deviceId}/device","order":4,"visible":true},{"id":"DeviceWorkbench","text":"Device Workbench","url":"#devices/{deviceId}/workbench","order":5,"visible":true},{"id":"ComplianceTestSuite","text":"Run Compliance Test Suite","url":"#devices/{deviceId}/execute-device-compliance-suite","order":6,"visible":true},{"id":"PerformActions","text":"Perform Actions","url":"#devices/{deviceId}/devicemodel/{deviceModelId}/device_actions","order":7,"visible":true},{"id":"PerformDiagnostics","text":"Perform Diagnostics","url":"#devices/{deviceId}/devicemodel/{deviceModelId}/diagnostics","order":8,"visible":true}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="WiFi 5Ghz" panelType="PANEL_DASHBOARD_SERVICE_CONFIG">
            <configuration>{"readOnly":false,"tabName":"5b081482-64dc-c72e-3ac8-f63479624e51","dataSource":{"type":"SERVICE_CONFIGURATION_SCRIPT","sourceId":"WiFi 5","sourceIdSet":[]},"diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_SERVICE_CONFIG","dataType":"SERVICE_CONFIGURATION_SCRIPT","dataSourceServiceConfig":"6e110c84-cf23-fb31-5500-b17786aa76c7"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.last_seen.name##" panelType="PANEL_STATUS_LASTSEEN">
            <configuration>{"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"duration":{"enable":false,"unit":null}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Wi-Fi Survey" panelType="PANEL_DASHBOARD_WIFISURVEY">
            <configuration>{"tabName":"5b081482-64dc-c72e-3ac8-f63479624e51","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_WIFISURVEY"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Dispositivos Conectados" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"7126f81f-501a-6888-c433-01e57632d3b3","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/17c6b210-8e8e-11eb-9808-f3ffb7f10f38?embed=true&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-48h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:'rgba(145,112,184,1)',fill:0.5,formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'Dispositivos%20Conectados',line_width:1,metrics:!((field:params.InternetGatewayDevice.LANDevice.1.Hosts.HostNumberOfEntries,id:'61ca57f2-469d-11e7-af02-69e470af7417',type:max)),point_size:1,separate_axis:0,split_color_mode:kibana,split_mode:everything,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'@timestamp',tooltip_mode:show_all,type:timeseries),title:'Dispositivos%20Conectados%20-%20Individual',type:metrics))"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Connected Devices Topology" panelType="PANEL_DASHBOARD_CONNECTED_DEVICES">
            <configuration>{"readOnly":false,"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"##dashboard.connected_devices_topology.name##","sourceIdSet":[]},"tabName":"c06638c6-7738-fe1a-b36f-0afc8c0f62ac","diagnosticsConfig":[{"diagnosticParameters":[]}]}</configuration>
        </dashboardPanel>
        <dashboardPanel name="TX" panelType="PANEL_STATUS_CUSTOM">
            <configuration>{"units":"db","rules":{"threshold":"DECREASING","ok":{"className":"ok","message":"OK"},"warning":{"className":"warning","message":"Atenção ","value":-25},"failure":{"className":"failure","message":"Critico","value":-27}},"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.X_ALU_OntOpticalParam.TXPower"},"category":"NUMERIC","limits":{}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Utilização de Canal  2.4Ghz" panelType="PANEL_DASHBOARD_KIBANA_IFRAME">
            <configuration>{"tabName":"5b081482-64dc-c72e-3ac8-f63479624e51","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_KIBANA_IFRAME","pixelHeight":"","url":"/acs/kibana/app/visualize#/edit/6badf9c0-902b-11ec-a070-35c390214c77?embed=true&amp;type=metrics&amp;_g=(filters:!(),refreshInterval:(pause:!t,value:0),time:(from:now-48h,to:now))&amp;_a=(filters:!(),linked:!f,query:(language:kuery,query:''),uiState:(),vis:(aggs:!(),params:(axis_formatter:number,axis_position:left,axis_scale:normal,default_index_pattern:'metricbeat-*',default_timefield:'@timestamp',filter:(language:kuery,query:'serial.keyword:{serialNumber}'),id:'61ca57f0-469d-11e7-af02-69e470af7417',index_pattern:'monitored-parameter*',interval:'',isModelInvalid:!f,series:!((axis_position:right,chart_type:line,color:%2368BC00,fill:'0.1',filter:(language:kuery,query:''),formatter:number,id:'61ca57f1-469d-11e7-af02-69e470af7417',label:'',line_width:1,metrics:!((id:'61ca57f2-469d-11e7-af02-69e470af7417',type:count)),point_size:1,separate_axis:0,split_color_mode:kibana,split_filters:!((color:%2368BC00,filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%201'),id:c0235550-902a-11ec-8823-65b10961c04e,label:'Canal%201'),(color:'rgba(84,179,153,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%202'),id:c94521e0-902a-11ec-8823-65b10961c04e,label:'Canal%202'),(color:'rgba(211,96,134,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%203'),id:d3408590-902a-11ec-8823-65b10961c04e,label:'Canal%203'),(color:'rgba(145,112,184,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%204'),id:d7d269c0-902a-11ec-8823-65b10961c04e,label:'Canal%204'),(color:'rgba(202,142,174,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%205'),id:dd5341d0-902a-11ec-8823-65b10961c04e,label:'Canal%205'),(color:'rgba(214,191,87,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%206'),id:e0a727c0-902a-11ec-8823-65b10961c04e,label:'Canal%206'),(color:'rgba(185,168,136,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%207'),id:e76b5540-902a-11ec-8823-65b10961c04e,label:'Canal%207'),(color:'rgba(218,139,69,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%208'),id:ea256c30-902a-11ec-8823-65b10961c04e,label:'Canal%208'),(color:'rgba(170,101,86,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%209'),id:eda32140-902a-11ec-8823-65b10961c04e,label:'Canal%209'),(color:'rgba(231,102,76,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%2010'),id:f106bea0-902a-11ec-8823-65b10961c04e,label:'Canal%2010'),(color:'rgba(22,0,188,1)',filter:(language:kuery,query:'params.InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.ChannelsInUse%20:%2011'),id:f3c1bff0-902a-11ec-8823-65b10961c04e,label:'Canal%2011')),split_mode:filters,stacked:none,type:timeseries)),show_grid:1,show_legend:1,time_field:'',tooltip_mode:show_all,type:timeseries),title:'Channel%202.4%20-%20Per%20Device',type:metrics))\n"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Broadband Speed Test" panelType="PANEL_DASHBOARD_BROADBAND_SPEED">
            <configuration>{"tabName":"b9777e26-8cc0-fa40-d5aa-56f19b104f92","diagnosticsConfig":[{"id":"Download Diagnostics","subType":"DOWNLOADSPEED","diagnosticParameters":[{"name":"InternetGatewayDevice.DownloadDiagnostics.DownloadURL","value":"http://35.215.210.14:9090/download.bin"},{"name":"InternetGatewayDevice.DownloadDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.DownloadDiagnostics.DSCP","value":""},{"name":"InternetGatewayDevice.DownloadDiagnostics.EthernetPriority","value":""}]},{"id":"Upload Diagnostics","subType":"UPLOADSPEED","diagnosticParameters":[{"name":"InternetGatewayDevice.UploadDiagnostics.EthernetPriority","value":""},{"name":"InternetGatewayDevice.UploadDiagnostics.UploadURL","value":"http://35.215.210.14:9090/upload.bin"},{"name":"InternetGatewayDevice.UploadDiagnostics.DSCP","value":""},{"name":"InternetGatewayDevice.UploadDiagnostics.Interface","value":""},{"name":"InternetGatewayDevice.UploadDiagnostics.TestFileLength","value":"1000"}]}],"panelSource":"PANEL_DASHBOARD_BROADBAND_SPEED","downloadEnabled":true,"uploadEnabled":true,"InternetGatewayDevice.DownloadDiagnostics.DownloadURL":"http://35.215.210.14:9090/download.bin","InternetGatewayDevice.DownloadDiagnostics.Interface":"","InternetGatewayDevice.DownloadDiagnostics.DSCP":"","InternetGatewayDevice.DownloadDiagnostics.EthernetPriority":"","InternetGatewayDevice.UploadDiagnostics.EthernetPriority":"","InternetGatewayDevice.UploadDiagnostics.UploadURL":"http://35.215.210.14:9090/upload.bin","InternetGatewayDevice.UploadDiagnostics.DSCP":"","InternetGatewayDevice.UploadDiagnostics.Interface":"","InternetGatewayDevice.UploadDiagnostics.TestFileLength":"1000"}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.up_time.name##" panelType="PANEL_STATUS_UPTIME">
            <configuration>{"dataSource":{"type":"DEVICE_PARAMETER","sourceId":"InternetGatewayDevice.DeviceInfo.UpTime","sourceIdSet":[]},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"name":"self"}}]},"duration":{"enable":true,"unit":"seconds"}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Connected Devices" panelType="PANEL_STATUS_CONNECTED">
            <configuration>{"rules":{"threshold":"INCREASING","ok":{"className":"ok","message":"OK"},"warning":{"className":"warning","message":"Atenção Crítico","value":50},"failure":{"className":"failure","message":"","value":70}},"units":"","limits":{}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Automated Troubleshooting" panelType="PANEL_DASHBOARD_TROUBLESHOOTING">
            <configuration>{"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"Automated Troubleshooting","sourceIdSet":[]},"readOnly":false,"tabName":"b78a2215-6f67-d319-411d-cd5e8da5a6b4","diagnosticsConfig":[{"diagnosticParameters":[]}],"panelSource":"PANEL_DASHBOARD_TROUBLESHOOTING","pixelHeight":""}</configuration>
        </dashboardPanel>
        <dashboardPanel name="Alerts" panelType="PANEL_STATUS_ALERTS">
            <configuration>{"rules":{"threshold":"NONE","ok":{"className":"ok"},"warning":{"className":"warning"},"failure":{"className":"failure"}},"category":"NUMERIC","limits":{}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.broadband_speed_hist.name##" panelType="PANEL_DASHBOARD_BROADBAND_HISTORICAL">
            <configuration>{"buttons":{"handlers":[{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"tableConfig":{"searchName":"PANEL_DASHBOARD_BROADBAND_HISTORICAL","title":"Historic Broadband Speed Test Results","searchParams":{"tableName":"DIAGNOSTIC_RESULT_SUMMARY","url":"/devices/{deviceId}/diagnostics/speedtest","q":"PINGTESTDATE is null","pageSize":20,"orderBy":"LASTMODIFIED","ascending":false},"columns":[{"name":"time","field":"lastModified","label":"Time","align":"left","dataType":"DATETIME","fieldFormat":"hh:mma, dd MMM yyyy"},{"name":"dload","field":"downloadSpeed","label":"Download Speed (Mbps)","align":"center","dataType":"MBYTES","fieldFormat":"%.1f"},{"name":"uload","field":"uploadSpeed","label":"Upload Speed (Mbps)","align":"center","dataType":"MBYTES","fieldFormat":"%.1f"}]}}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.tr069_config.name##" panelType="PANEL_DASHBOARD_TR069_CONFIG">
            <configuration>{"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"##dashboard.tr069_config.name##","sourceIdSet":[]},"buttons":{"handlers":[{"text":"Save","handler":"saveServiceConfigParameters","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"POST"},"visible":true,"tab":null},{"text":"Cancel","handler":"cancel","endpoint":{"url":"/deviceoperations/cancellation","verb":"POST"},"visible":false,"tab":null},{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"readOnly":false}</configuration>
        </dashboardPanel>
        <dashboardPanel name="##dashboard.device_info.name##" panelType="PANEL_DASHBOARD_DEVICE_INFO">
            <configuration>{"dataSource":{"type":"DASHBOARD_SCRIPT","sourceId":"##dashboard.device_info.name##","sourceIdSet":[]},"websocket":{"handlers":[{"type":"PANEL_UPDATE","field":"panelData.value","filter":{"panelType":"PANEL_STATUS_ONLINE"}}]},"buttons":{"handlers":[{"text":"Refresh","handler":"refresh","endpoint":{"url":"/devices/{deviceId}/dashboard/panels?id={panelId}","verb":"GET"},"visible":true,"tab":null}]},"readOnly":true}</configuration>
        </dashboardPanel>
    </dashboardPanels>
    <dashboardLayout>{"version":"1.2","children":[{"type":"COLUMN_LEFT","order":0,"hasPanelChildren":false,"children":[{"name":"##dashboard.layout.region.device_ident##","type":"REGION_DEVICE_IDENTIFIER","order":0,"hasPanelChildren":false,"children":[{"name":"PANEL_COMMON_DEVICE_IDENTIFIER","type":"PANEL_COMMON_DEVICE_IDENTIFIER","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.customer_ident##","type":"REGION_CUSTOMER_IDENTIIFIER","order":1,"hasPanelChildren":true,"children":[{"name":"PANEL_COMMON_CUSTOMER_IDENTIFIER","type":"PANEL_COMMON_CUSTOMER_IDENTIFIER","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.images##","type":"REGION_DEVICE_IMAGES","order":2,"hasPanelChildren":true,"children":[{"name":"PANEL_COMMON_DEVICE_IMAGES","type":"PANEL_COMMON_DEVICE_IMAGES","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.operations##","type":"REGION_DEVICE_OPERATIONS","order":3,"hasPanelChildren":true,"children":[{"name":"##dashboard.device_actions.name##","type":"PANEL_DEVICE_OPERATIONS_ACTIONS","order":0,"hasPanelChildren":false},{"name":"##dashboard.common_issues.name##","type":"PANEL_DEVICE_OPERATIONS_ISSUES","order":1,"hasPanelChildren":false},{"name":"##dashboard.admin_actions.name##","type":"PANEL_DEVICE_OPERATIONS_ADMIN","order":2,"hasPanelChildren":false}]}]},{"type":"COLUMN_RIGHT","order":1,"hasPanelChildren":false,"children":[{"name":"##dashboard.layout.region.status##","type":"REGION_STATUS","order":0,"hasPanelChildren":true,"children":[{"name":"##dashboard.online.name##","type":"PANEL_STATUS_ONLINE","order":0,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.last_seen.name##","type":"PANEL_STATUS_LASTSEEN","order":1,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.sync_status.name##","type":"PANEL_STATUS_SYNC","order":2,"hasPanelChildren":false,"visible":true},{"name":"Connected Devices","type":"PANEL_STATUS_CONNECTED","order":3,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.active_operations.name##","type":"PANEL_STATUS_OPERATIONS_ACTIVE","order":4,"hasPanelChildren":false,"visible":true},{"name":"##dashboard.up_time.name##","type":"PANEL_STATUS_UPTIME","order":5,"hasPanelChildren":false,"visible":true},{"name":"TX","type":"PANEL_STATUS_CUSTOM","order":6,"hasPanelChildren":false,"visible":true,"category":"NUMERIC"},{"name":"RX","type":"PANEL_STATUS_CUSTOM","order":7,"hasPanelChildren":false,"visible":true,"category":"NUMERIC"},{"name":"CPU %","type":"PANEL_STATUS_CUSTOM","order":8,"hasPanelChildren":false,"visible":true,"category":"NUMERIC"},{"name":"Memória","type":"PANEL_STATUS_CUSTOM","order":9,"hasPanelChildren":false,"visible":true,"category":"NUMERIC"},{"name":"Temperatura","type":"PANEL_STATUS_CUSTOM","order":10,"hasPanelChildren":false,"visible":true,"category":"NUMERIC"},{"name":"WAN Connection","type":"PANEL_STATUS_CUSTOM","order":11,"hasPanelChildren":false,"visible":true,"category":"ENUM"},{"name":"MTU","type":"PANEL_STATUS_CUSTOM","order":12,"hasPanelChildren":false,"visible":true,"category":"NUMERIC"},{"name":"##dashboard.failed_operations.name##","type":"PANEL_STATUS_OPERATIONS_FAILED","order":13,"hasPanelChildren":false,"visible":true},{"name":"Alerts","type":"PANEL_STATUS_ALERTS","order":14,"hasPanelChildren":false,"visible":true}]},{"name":"##dashboard.layout.region.csr_call_log##","type":"REGION_CSR_CALL_INFO","order":1,"hasPanelChildren":true,"children":[{"name":"##dashboard.csr_call_info.name##","type":"PANEL_COMMON_CSR_CALL_INFO","order":0,"hasPanelChildren":false}]},{"name":"##dashboard.layout.region.dashboards##","type":"REGION_DASHBOARDS","order":2,"hasPanelChildren":false,"children":[{"name":"##dashboard.tab.overview##","type":"TAB_DASHBOARD","order":0,"hasPanelChildren":true,"visible":true,"children":[{"name":"Broadband Speed Test","type":"PANEL_DASHBOARD_BROADBAND_SPEED","order":0,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"##dashboard.broadband_speed_hist.name##","type":"PANEL_DASHBOARD_BROADBAND_HISTORICAL","order":1,"hasPanelChildren":false,"visible":true,"size":{"h":1,"v":1}},{"name":"##dashboard.session_info.name##","type":"PANEL_DASHBOARD_SESSION_INFO","order":2,"hasPanelChildren":false,"visible":true,"size":{"h":1,"v":1}},{"name":"##dashboard.device_info.name##","type":"PANEL_DASHBOARD_DEVICE_INFO","order":3,"hasPanelChildren":false,"visible":true,"size":{"h":1,"v":1}}]},{"name":"##dashboard.tab.topology##","type":"TAB_DASHBOARD","order":1,"hasPanelChildren":true,"visible":false,"children":[{"name":"Connected Devices Topology","type":"PANEL_DASHBOARD_CONNECTED_DEVICES","order":0,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}}]},{"name":"##dashboard.tab.diagnostics##","type":"TAB_DASHBOARD","order":2,"hasPanelChildren":true,"visible":false,"children":[{"name":"##dashboard.tr069_config.name##","type":"PANEL_DASHBOARD_TR069_CONFIG","order":0,"hasPanelChildren":false,"size":{"h":1,"v":1}},{"name":"IP Ping Test","type":"PANEL_DASHBOARD_IPPING","order":1,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"Trace Route","type":"PANEL_DASHBOARD_TRACEROUTE","order":2,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}}]},{"name":"WiFi","type":"TAB_DASHBOARD","order":3,"hasPanelChildren":true,"visible":true,"children":[{"name":"WiFi 2.4Ghz","type":"PANEL_DASHBOARD_SERVICE_CONFIG","order":0,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"WiFi 5Ghz","type":"PANEL_DASHBOARD_SERVICE_CONFIG","order":1,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":1,"v":1}},{"name":"Wi-Fi Survey","type":"PANEL_DASHBOARD_WIFISURVEY","order":2,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Tráfego 2.4Ghz","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":3,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Utilização de Canal  2.4Ghz","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":4,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Pacotes Descartados 2.4Ghz","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":5,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"WiFi Tráfego 5Ghz","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":6,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Utilização Canal 5Ghz","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":7,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Pacotes Descartados 5Ghz","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":8,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}}]},{"name":"Troubleshooting","type":"TAB_DASHBOARD","order":4,"hasPanelChildren":true,"visible":true,"children":[{"name":"Automated Troubleshooting","type":"PANEL_DASHBOARD_TROUBLESHOOTING","order":0,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":2}}]},{"name":"Gráficos","type":"TAB_DASHBOARD","order":5,"hasPanelChildren":true,"visible":true,"children":[{"name":"Uptime","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":0,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Utilização CPU","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":1,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Memória Livre","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":2,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Níveis TX/RX","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":3,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}},{"name":"Dispositivos Conectados","type":"PANEL_DASHBOARD_KIBANA_IFRAME","order":4,"hasPanelChildren":false,"visible":true,"size":{"type":"grid","h":0,"v":1}}]}]}]}]}</dashboardLayout>
    <imageReferences friendlyName="1425ga.png" extension="png" description="" index="0" fileName="1425ga.png.png"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.ErrorsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.ErrorsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UPnP.Device.Enable" elementDefinition="InternetGatewayDevice.UPnP.Device.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.DuplexMode" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.DuplexMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallWaitingEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallWaitingEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.MaxAssocUsers" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.MaxAssocUsers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.MaxAssocUsers" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.Features" elementDefinition="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.Features" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.CallingNumber" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.CallingNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.CallingNumber" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6PrefixOrigin" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6PrefixOrigin" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6PrefixOrigin" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UserInterface.ButtonTextColor" elementDefinition="InternetGatewayDevice.UserInterface.ButtonTextColor" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.IncomingCallsAnswered" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.IncomingCallsAnswered" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.NetMonitorDiagnostics.RESV2" elementDefinition="InternetGatewayDevice.NetMonitorDiagnostics.RESV2" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.NetMonitorDiagnostics.RESV2" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MACAddressControlEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MACAddressControlEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.NetMonitorDiagnostics.RESV1" elementDefinition="InternetGatewayDevice.NetMonitorDiagnostics.RESV1" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.NetMonitorDiagnostics.RESV1" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.Enable" elementDefinition="InternetGatewayDevice.UDPEchoConfig.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.PINStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.PINStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.PINStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.DelayBetweenRetries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.DelayBetweenRetries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_WarmLineEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_WarmLineEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_WarmLineEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU_OntOpticalParam.RXPowerUpper" elementDefinition="InternetGatewayDevice.X_ALU_OntOpticalParam.RXPowerUpper" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU_OntOpticalParam.RXPowerUpper" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MiniLenPrompt" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MiniLenPrompt" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MiniLenPrompt" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.Username" elementDefinition="InternetGatewayDevice.ManagementServer.Username" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UploadTransports" elementDefinition="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UploadTransports" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDeviceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDeviceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.X_ALU_COM_CurDuplexMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.X_ALU_COM_CurDuplexMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.X_ALU_COM_CurDuplexMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Ringer_TestResult" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Ringer_TestResult" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Ringer_TestResult" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.TimeFirstPacketReceived" elementDefinition="InternetGatewayDevice.UDPEchoConfig.TimeFirstPacketReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_BulkData.ProfileNumberOfEntries" elementDefinition="InternetGatewayDevice.X_ALU-COM_BulkData.ProfileNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_BulkData.ProfileNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_DHCPv6Server.MinAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_DHCPv6Server.MinAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_DHCPv6Server.MinAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.Message" elementDefinition="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.Message" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.Message" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.FileSystem" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.FileSystem" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.NetworkServer.SMBEnable" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.NetworkServer.SMBEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DefaultGateway" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DefaultGateway" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKeyIndex" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKeyIndex" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.DataBackupMode" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.DataBackupMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.DataBackupMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_PwrMngtCfg.X_ALU-COM_PSMEnable" elementDefinition="InternetGatewayDevice.X_ALU-COM_PwrMngtCfg.X_ALU-COM_PSMEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_PwrMngtCfg.X_ALU-COM_PSMEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.SentDHCPOption.{i}.Value" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.SentDHCPOption.{i}.Value" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.LocalPortMax" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.LocalPortMax" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_FarEndPacketLossRate" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_FarEndPacketLossRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_FarEndPacketLossRate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UserInterface.ISPHomePage" elementDefinition="InternetGatewayDevice.UserInterface.ISPHomePage" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTServerGroupID" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTServerGroupID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTServerGroupID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACFromVendorClassIDFilter" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACFromVendorClassIDFilter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.Enable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.activeModeEnabled" elementDefinition="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.activeModeEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.activeModeEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU_COM_IsGuestSSID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU_COM_IsGuestSSID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU_COM_IsGuestSSID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.GRE.X_ALU-COM_Enable" elementDefinition="InternetGatewayDevice.GRE.X_ALU-COM_Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.GRE.X_ALU-COM_Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.IncrementalResultNumberOfEntries" elementDefinition="InternetGatewayDevice.UploadDiagnostics.IncrementalResultNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.IncrementalResultNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.Transports" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.Transports" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterStatus" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.X_ALU-COM_SessionMinSE" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.X_ALU-COM_SessionMinSE" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.X_ALU-COM_SessionMinSE" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Port" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Port" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Port" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.PortUsed" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.PortUsed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.PortUsed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPSSID5" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPSSID5" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPSSID5" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.OperationalDataTransmitRates" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.OperationalDataTransmitRates" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallState" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallState" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ALU-COM_RingSchedule.Enable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ALU-COM_RingSchedule.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ALU-COM_RingSchedule.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_RouterAdvertisement.AdvOtherConfigFlag" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_RouterAdvertisement.AdvOtherConfigFlag" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_RouterAdvertisement.AdvOtherConfigFlag" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.Description" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.Description" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.Description" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnectionNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.SupportedAccessTechnologies" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.SupportedAccessTechnologies" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.SupportedAccessTechnologies" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetUnknownProtoPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetUnknownProtoPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU_OntOpticalParam.LowerTransmitPowerThreshold" elementDefinition="InternetGatewayDevice.X_ALU_OntOpticalParam.LowerTransmitPowerThreshold" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU_OntOpticalParam.LowerTransmitPowerThreshold" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalAssociations" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalAssociations" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_TrustedRemoteServer.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_TrustedRemoteServer.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_TrustedRemoteServer.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACFromUserClassIDFilterExclude" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACFromUserClassIDFilterExclude" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_MACAddressControlMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_MACAddressControlMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_MACAddressControlMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.MaximumNumberOfDigits" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.MaximumNumberOfDigits" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.DistanceFromRoot" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.DistanceFromRoot" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Description" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Description" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Name" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Firewall.Config" elementDefinition="InternetGatewayDevice.Firewall.Config" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.PacketsReceived" elementDefinition="InternetGatewayDevice.UDPEchoConfig.PacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.PasswordRequired" elementDefinition="InternetGatewayDevice.UserInterface.PasswordRequired" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPOptionNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPOptionNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.XMPP.ConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.XMPP.ConnectionNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ProcessStatus.ProcessNumberOfEntries" elementDefinition="InternetGatewayDevice.DeviceInfo.ProcessStatus.ProcessNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDeviceNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDeviceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_DC_Voltage_Tip_Ground-Volt" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_DC_Voltage_Tip_Ground-Volt" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_DC_Voltage_Tip_Ground-Volt" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.GatekeeperID" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.GatekeeperID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.NumberOfRetries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.NumberOfRetries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsReceivedUnicast" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsReceivedUnicast" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsReceivedUnicast" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPLeaseTime" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPLeaseTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UPSAlarm.BatteryLow" elementDefinition="InternetGatewayDevice.X_ALU-COM_UPSAlarm.BatteryLow" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UPSAlarm.BatteryLow" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingKey" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingKey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.Enable" elementDefinition="InternetGatewayDevice.Time.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PreSharedKey.{i}.AssociatedDeviceMACAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PreSharedKey.{i}.AssociatedDeviceMACAddress" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.OperatingFrequencyBand" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.OperatingFrequencyBand" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.OperatingFrequencyBand" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceConfig.PersistentData" elementDefinition="InternetGatewayDevice.DeviceConfig.PersistentData" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_ReversePower.VoltageThreshold" elementDefinition="InternetGatewayDevice.X_ALU-COM_ReversePower.VoltageThreshold" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_ReversePower.VoltageThreshold" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.ServerIPAddr" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.ServerIPAddr" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.ServerIPAddr" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Clientkey" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Clientkey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Clientkey" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU_COM_AutoLaunchSelfTestEnable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU_COM_AutoLaunchSelfTestEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU_COM_AutoLaunchSelfTestEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.PIN" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.PIN" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.PIN" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallReturnEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallReturnEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Status" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Status" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU_OntOpticalParam.TransceiverTemperature" elementDefinition="InternetGatewayDevice.X_ALU_OntOpticalParam.TransceiverTemperature" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU_OntOpticalParam.TransceiverTemperature" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.RadioEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.RadioEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DSCP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.Alias" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.Alias" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Ookla.Interface" elementDefinition="InternetGatewayDevice.X_ALU-COM_Ookla.Interface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Ookla.Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_Authentication.WebAccount.UserName" elementDefinition="InternetGatewayDevice.X_Authentication.WebAccount.UserName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.WebAccount.UserName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.DiscardPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.DiscardPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicAuthenticationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicAuthenticationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.SessionStartTime" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.SessionStartTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.UserAccountNumberOfEntries" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.UserAccountNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Connection.{i}.ActiveConnectionServiceID" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Connection.{i}.ActiveConnectionServiceID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.RFOutPower" elementDefinition="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.RFOutPower" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.RFOutPower" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Location_Information" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Location_Information" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Location_Information" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadTransports" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DownloadTransports" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.DownloadTransports" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AccessPoint.Username" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AccessPoint.Username" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AccessPoint.Username" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalBytesReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_CalledNumber" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_CalledNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_CalledNumber" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.UplinkDetectMethod" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.UplinkDetectMethod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.UplinkDetectMethod" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.ExternalAntennaEnable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.ExternalAntennaEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.ExternalAntennaEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ParameterKey" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ParameterKey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ParameterKey" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadDiagnosticsMaxIncrementalResult" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DownloadDiagnosticsMaxIncrementalResult" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.DownloadDiagnosticsMaxIncrementalResult" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANUSBInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANUSBInterfaceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Certificate" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Certificate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Certificate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_RoundTripDelay" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_RoundTripDelay" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_RoundTripDelay" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.IMSI" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.IMSI" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.IMSI" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACFromUserClassIDFilter" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACFromUserClassIDFilter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.X_ALU-COM_Option82SSIDEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.X_ALU-COM_Option82SSIDEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.X_ALU-COM_Option82SSIDEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanNameType" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanNameType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanNameType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.Codecs.{i}.SilenceSuppression" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.Codecs.{i}.SilenceSuppression" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ProductClass" elementDefinition="InternetGatewayDevice.DeviceInfo.ProductClass" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.DefaultConnectionService" elementDefinition="InternetGatewayDevice.Layer3Forwarding.DefaultConnectionService" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsSentMulticast" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsSentMulticast" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsSentMulticast" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AppCfg.OperatorPlugins.plugin.{i}.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_AppCfg.OperatorPlugins.plugin.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AppCfg.OperatorPlugins.plugin.{i}.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBytesSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBytesSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UPSAlarm.BatteryMissing" elementDefinition="InternetGatewayDevice.X_ALU-COM_UPSAlarm.BatteryMissing" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UPSAlarm.BatteryMissing" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UPnP.Discovery.ServiceNumberOfEntries" elementDefinition="InternetGatewayDevice.UPnP.Discovery.ServiceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.EventSubscribe.{i}.Notifier" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.EventSubscribe.{i}.Notifier" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.EventClearedTime" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.EventClearedTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.EventClearedTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.LocalPortMin" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.LocalPortMin" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MaxAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MaxAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_DownStreamFragments" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_DownStreamFragments" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_DownStreamFragments" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.L2TPStartMaxRetry" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.L2TPStartMaxRetry" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.L2TPStartMaxRetry" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TotalBytesSent" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TotalBytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.NSLookupDiagnostics.HostName" elementDefinition="InternetGatewayDevice.NSLookupDiagnostics.HostName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.UploadTransports" elementDefinition="InternetGatewayDevice.UploadDiagnostics.UploadTransports" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.UploadTransports" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.PreferredAccessTechnology" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.PreferredAccessTechnology" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.PreferredAccessTechnology" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.TrySwitchTimes" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.TrySwitchTimes" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.TrySwitchTimes" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UserInterface.ISPMailServer" elementDefinition="InternetGatewayDevice.UserInterface.ISPMailServer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.ProxyServerPort" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.ProxyServerPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU_COM_ChannelWidth" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU_COM_ChannelWidth" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU_COM_ChannelWidth" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetMulticastPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetMulticastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Name" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_ALU-COM_VLANIDMark" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_ALU-COM_VLANIDMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_ALU-COM_VLANIDMark" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Enable" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AppCfg.X_EquipmentIdentity.X_CMEI.HeartbeatCycle" elementDefinition="InternetGatewayDevice.X_ALU-COM_AppCfg.X_EquipmentIdentity.X_CMEI.HeartbeatCycle" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AppCfg.X_EquipmentIdentity.X_CMEI.HeartbeatCycle" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.HTTPWritable" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.HTTPWritable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.HTTPWritable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_Authentication.TelnetSshAccount.UserName" elementDefinition="InternetGatewayDevice.X_Authentication.TelnetSshAccount.UserName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.TelnetSshAccount.UserName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.UpgradesManaged" elementDefinition="InternetGatewayDevice.ManagementServer.UpgradesManaged" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.OutgoingCallsFailed" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.OutgoingCallsFailed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.MulticastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.MulticastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_ALU-COM_WANUSBDongleLinkConfig.LinkStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_ALU-COM_WANUSBDongleLinkConfig.LinkStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_ALU-COM_WANUSBDongleLinkConfig.LinkStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Standard" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Standard" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.PINCheck" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.PINCheck" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.PINCheck" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.RemoteLoopbackEnabled" elementDefinition="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.RemoteLoopbackEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.RemoteLoopbackEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.OutgoingCallsAnswered" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.OutgoingCallsAnswered" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SignalStrength" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SignalStrength" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SignalStrength" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.PeerSubnet" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.PeerSubnet" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.PeerSubnet" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.ROMTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.ROMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.Enable" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.List.{i}.EntryID" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.List.{i}.EntryID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallForwardOnNoAnswerRingCount" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallForwardOnNoAnswerRingCount" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Operator_Name" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Operator_Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Operator_Name" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.FileBasedRingGeneration" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.FileBasedRingGeneration" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNPassword" elementDefinition="InternetGatewayDevice.ManagementServer.STUNPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.Alias" elementDefinition="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.Alias" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UPSAlarm.BatteryFailure" elementDefinition="InternetGatewayDevice.X_ALU-COM_UPSAlarm.BatteryFailure" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UPSAlarm.BatteryFailure" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.Codecs.{i}.Codec" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.Codecs.{i}.Codec" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceServiceNumberOfEntries" elementDefinition="InternetGatewayDevice.Services.VoiceServiceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPv4UploadDiagnosticsSupported" elementDefinition="InternetGatewayDevice.IPv4UploadDiagnosticsSupported" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.IPv4UploadDiagnosticsSupported" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.PINCheck" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.PINCheck" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.PINCheck" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU_Option125Value" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU_Option125Value" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU_Option125Value" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.Timeout" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.Timeout" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.Timeout" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.SshDisabled" elementDefinition="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.SshDisabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.SshDisabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Stats.PacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Stats.PacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Stats.PacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_ReversePower.CurrentThreshold" elementDefinition="InternetGatewayDevice.X_ALU-COM_ReversePower.CurrentThreshold" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_ReversePower.CurrentThreshold" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACFromUserClassIDFilter" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACFromUserClassIDFilter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_Authentication.WebAccount.Priority" elementDefinition="InternetGatewayDevice.X_Authentication.WebAccount.Priority" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.WebAccount.Priority" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.DataBlockSize" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.DataBlockSize" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.DataBlockSize" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.IdleTimeout" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.IdleTimeout" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.IdleTimeout" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.LastConfigurationError" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.LastConfigurationError" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU_COM_BandSteering.RSSIHighUpSteer" elementDefinition="InternetGatewayDevice.X_ALU_COM_BandSteering.RSSIHighUpSteer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU_COM_BandSteering.RSSIHighUpSteer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Reset" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Reset" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.PeerSubnetMask" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.PeerSubnetMask" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.PeerSubnetMask" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.BroadcastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.BroadcastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallForwardOnBusyEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallForwardOnBusyEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.MgtDNS" elementDefinition="InternetGatewayDevice.ManagementServer.MgtDNS" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.MgtDNS" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.WorkMode" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.WorkMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.WorkMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Ringer.Event.{i}.Function" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Ringer.Event.{i}.Function" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_AC_Voltage_Ring_Ground-Volt" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_AC_Voltage_Ring_Ground-Volt" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_AC_Voltage_Ring_Ground-Volt" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.List.{i}.Priority" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.List.{i}.Priority" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterfaceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.ProxyServer" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.ProxyServer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.X_ALU_COM_XMPP_Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.X_ALU_COM_XMPP_Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.X_ALU_COM_XMPP_Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsErrored" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsErrored" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsErrored" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Stats.PacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Stats.PacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Stats.PacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPv4ServerSelectionDiagnosticsSupported" elementDefinition="InternetGatewayDevice.IPv4ServerSelectionDiagnosticsSupported" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.IPv4ServerSelectionDiagnosticsSupported" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.PeriodicInformInterval" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.PeriodicInformInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.PeriodicInformInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPRouters" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPRouters" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_SessionSuccessful" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_SessionSuccessful" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_SessionSuccessful" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Authentication" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Authentication" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Authentication" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.InterTransmissionTime" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.InterTransmissionTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.InterTransmissionTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.CallAgent2" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.CallAgent2" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.CallAgent1" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.CallAgent1" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.PerceivedSeverity" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.PerceivedSeverity" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.PerceivedSeverity" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPStaticAddress.{i}.Yiaddr" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPStaticAddress.{i}.Yiaddr" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.TLSAuthenticationKeySizes" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.TLSAuthenticationKeySizes" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.LCPEchoInterval" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.LCPEchoInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.LCPEchoInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsReceivedBroadcast" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsReceivedBroadcast" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsReceivedBroadcast" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.OutgoingCallsAttempted" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.OutgoingCallsAttempted" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterEnable" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPacketsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.TrustedNetworkEnable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.TrustedNetworkEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.TrustedNetworkEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.SIP.AuthUserName" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.SIP.AuthUserName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnicastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnicastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsReceivedUnicast" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsReceivedUnicast" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsReceivedUnicast" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.RingFileFormats" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.RingFileFormats" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.MaximumResponseTime" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.MaximumResponseTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.MaximumResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_DSCPMark" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_DSCPMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_DSCPMark" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAEncryptionModes" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAEncryptionModes" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.AutoCreateInstances" elementDefinition="InternetGatewayDevice.ManagementServer.AutoCreateInstances" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_ReversePower.VoltagePercent" elementDefinition="InternetGatewayDevice.X_ALU-COM_ReversePower.VoltagePercent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_ReversePower.VoltagePercent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_RGCounters.USPacketLossCounter" elementDefinition="InternetGatewayDevice.X_ALU-COM_RGCounters.USPacketLossCounter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_RGCounters.USPacketLossCounter" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WLANPWDStats.Prompted" elementDefinition="InternetGatewayDevice.WLANPWDStats.Prompted" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WLANPWDStats.Prompted" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EtsiPse.Current" elementDefinition="InternetGatewayDevice.X_ALU-COM_EtsiPse.Current" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EtsiPse.Current" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.EthertypeFilterExclude" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.EthertypeFilterExclude" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.NSLookupDiagnostics.ResultNumberOfEntries" elementDefinition="InternetGatewayDevice.NSLookupDiagnostics.ResultNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_RGCounters.DSThroughputCounter" elementDefinition="InternetGatewayDevice.X_ALU-COM_RGCounters.DSThroughputCounter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_RGCounters.DSThroughputCounter" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.SupportedFileSystemTypes" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.SupportedFileSystemTypes" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.SupportedFileSystemTypes" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ASB_COM_EthPort.EthPortNum" elementDefinition="InternetGatewayDevice.X_ASB_COM_EthPort.EthPortNum" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ASB_COM_EthPort.EthPortNum" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_CallHoldEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_CallHoldEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_CallHoldEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.FaxT38.TCFMethod" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.FaxT38.TCFMethod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.MinimumResponseTime" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.MinimumResponseTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.MinimumResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.IPVer" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.IPVer" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.TraceRouteDiagnostics.IPVer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.PhyReferenceList" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.PhyReferenceList" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.ToneGeneration" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.ToneGeneration" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SRTPEncryptionKeySizes" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SRTPEncryptionKeySizes" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.ManagementIdleDisconnectTime" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.ManagementIdleDisconnectTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.ManagementIdleDisconnectTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.IncomingCallsConnected" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.IncomingCallsConnected" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_UpStreamFragments" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_UpStreamFragments" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_UpStreamFragments" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_WifiSchedule.Flag" elementDefinition="InternetGatewayDevice.X_ALU-COM_WifiSchedule.Flag" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_WifiSchedule.Flag" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenResponseTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TCPOpenResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.NetworkRequested" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.NetworkRequested" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.NetworkRequested" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.H323.H235AuthenticationMethods" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.H323.H235AuthenticationMethods" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ConnectionStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ConnectionStatus" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerConfigurable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPServerConfigurable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_AverageReceiveInterarrivalJitter" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_AverageReceiveInterarrivalJitter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_AverageReceiveInterarrivalJitter" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.URL" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.URL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.URL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.X_ALU_COM_TR111Enabled" elementDefinition="InternetGatewayDevice.ManagementServer.X_ALU_COM_TR111Enabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.X_ALU_COM_TR111Enabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.IMEI" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.IMEI" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.IMEI" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.Status" elementDefinition="InternetGatewayDevice.Time.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.RegistrationPeriod" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.RegistrationPeriod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SupportedDataTransferRates" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SupportedDataTransferRates" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SupportedDataTransferRates" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.ZwaveFWVersion" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.ZwaveFWVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.ZwaveFWVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.X_ALU-COM_SessionExpires" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.X_ALU-COM_SessionExpires" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.X_ALU-COM_SessionExpires" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.FacilityActionArgument" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.FacilityActionArgument" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallForwardOnNoAnswerNumber" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallForwardOnNoAnswerNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ManageableDeviceNumberOfEntries" elementDefinition="InternetGatewayDevice.ManagementServer.ManageableDeviceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.ChatSupport" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.ChatSupport" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.ChatSupport" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.RSSI" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.RSSI" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.RSSI" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.TelnetTrusted" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.TelnetTrusted" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.TelnetTrusted" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_Authentication.Account.Password" elementDefinition="InternetGatewayDevice.X_Authentication.Account.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.Account.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.DSCP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.TunnelMode" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.TunnelMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.TunnelMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SupportedFrequencyBands" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SupportedFrequencyBands" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SupportedFrequencyBands" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPStaticAddress.{i}.Chaddr" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPStaticAddress.{i}.Chaddr" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.DTMFMethodG711" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.DTMFMethodG711" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.ManufacturerInfo.HardwareVersion" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.ManufacturerInfo.HardwareVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.ManufacturerInfo.HardwareVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigMethodsSupported" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigMethodsSupported" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.SftpDisabled" elementDefinition="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.SftpDisabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.SftpDisabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.UseCodecPriorityInSDPResponse" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.UseCodecPriorityInSDPResponse" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_UpStreamBwUtilization" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_UpStreamBwUtilization" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_UpStreamBwUtilization" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.Enable" elementDefinition="InternetGatewayDevice.QueueManagement.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.BulkData.Profile.{i}.HTTP.{i}.URL" elementDefinition="InternetGatewayDevice.BulkData.Profile.{i}.HTTP.{i}.URL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.BulkData.Profile.{i}.HTTP.{i}.URL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EtsiPse.PartnerClass" elementDefinition="InternetGatewayDevice.X_ALU-COM_EtsiPse.PartnerClass" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EtsiPse.PartnerClass" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AppCfg.DnsProxyCfg.X_ALU-COM_EDNS0" elementDefinition="InternetGatewayDevice.X_ALU-COM_AppCfg.DnsProxyCfg.X_ALU-COM_EDNS0" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AppCfg.DnsProxyCfg.X_ALU-COM_EDNS0" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EtsiPse.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_EtsiPse.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EtsiPse.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.InboundAuthUsername" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.InboundAuthUsername" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_SwMgnt.X_ALU-COM_PrefActivation_Time" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_SwMgnt.X_ALU-COM_PrefActivation_Time" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_SwMgnt.X_ALU-COM_PrefActivation_Time" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.MinimumNumberOfDigits" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.MinimumNumberOfDigits" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPSEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPSEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPSEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MESH_WDSHideSSID.KeyPassphrase2G" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MESH_WDSHideSSID.KeyPassphrase2G" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MESH_WDSHideSSID.KeyPassphrase2G" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.DialTone" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.DialTone" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.PhoneSupport" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.PhoneSupport" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.PhoneSupport" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.HttpDisabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.HttpDisabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.HttpDisabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.AverageReceiveInterarrivalJitter" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.AverageReceiveInterarrivalJitter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.PeriodicInformTime" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.PeriodicInformTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.PeriodicInformTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.TotalBytesSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.TotalBytesSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.TotalBytesSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.FirmwareVersion" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.FirmwareVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.FirmwareVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.SwManagedByOperator" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.SwManagedByOperator" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.SwManagedByOperator" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.MulticastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.MulticastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.UsbPrinterPassword" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.UsbPrinterPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.UsbPrinterPassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AutoPortBind.X_ALU-COM_AutoPortBindEnable" elementDefinition="InternetGatewayDevice.X_ALU-COM_AutoPortBind.X_ALU-COM_AutoPortBindEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AutoPortBind.X_ALU-COM_AutoPortBindEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.IncrementalResultNumberOfEntries" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.IncrementalResultNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.IncrementalResultNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.PrefixInformation.{i}.Mode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.PrefixInformation.{i}.Mode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.PrefixInformation.{i}.Mode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.DebugDyPass.PassLen" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.DebugDyPass.PassLen" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.DebugDyPass.PassLen" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnknownProtoPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnknownProtoPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MESH_WDSHideSSID.KeyPassphrase5G" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MESH_WDSHideSSID.KeyPassphrase5G" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MESH_WDSHideSSID.KeyPassphrase5G" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallerIDEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallerIDEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACAddressFilterExclude" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACAddressFilterExclude" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MACAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MACAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.ReceiveBitRate" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.ReceiveBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_GPON.RFOutputNumberOfEntries" elementDefinition="InternetGatewayDevice.X_ALU-COM_GPON.RFOutputNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_GPON.RFOutputNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_PacketsReceived" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_PacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_PacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_NetworkProperties.TcpSessionTimer" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_NetworkProperties.TcpSessionTimer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_NetworkProperties.TcpSessionTimer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.NetworkInUse" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.NetworkInUse" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.NetworkInUse" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.IMEI" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.IMEI" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.IMEI" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.RSSI" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.RSSI" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.RSSI" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_PortUsed" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_PortUsed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_PortUsed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.EventSubscribe.{i}.NotifierPort" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.EventSubscribe.{i}.NotifierPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TestBytesSent" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TestBytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TestBytesSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.SameCharRule" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.SameCharRule" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.SameCharRule" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.BytesSent" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.BytesSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.IPv6DNSServers" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.IPv6DNSServers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.IPv6DNSServers" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.ErrorsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.ErrorsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Venue_Class" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Venue_Class" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Venue_Class" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.SoftwareModules.ExecEnv.{i}.AllocatedMemory" elementDefinition="InternetGatewayDevice.SoftwareModules.ExecEnv.{i}.AllocatedMemory" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.TLSEncryptionKeySizes" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.TLSEncryptionKeySizes" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.ButtonColor" elementDefinition="InternetGatewayDevice.UserInterface.ButtonColor" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.SoftwareModules.ExecutionUnitNumberOfEntries" elementDefinition="InternetGatewayDevice.SoftwareModules.ExecutionUnitNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.GRE.X_ALU-COM_TunnelMode" elementDefinition="InternetGatewayDevice.GRE.X_ALU-COM_TunnelMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.GRE.X_ALU-COM_TunnelMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.GRE.X_ALU-COM_Opt82RemoteID" elementDefinition="InternetGatewayDevice.GRE.X_ALU-COM_Opt82RemoteID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.GRE.X_ALU-COM_Opt82RemoteID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.VLANIDUntag" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.VLANIDUntag" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.SFTPCapable" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.SFTPCapable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.SFTPCapable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ExactDigitMapEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ExactDigitMapEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ExactDigitMapEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LoopbackDetection.EthernetType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LoopbackDetection.EthernetType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LoopbackDetection.EthernetType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.PeriodicInformEnable" elementDefinition="InternetGatewayDevice.ManagementServer.PeriodicInformEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_UnderSizePacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_UnderSizePacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_UnderSizePacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.OperatingChannelBandwidth" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.OperatingChannelBandwidth" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.OperatingChannelBandwidth" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.GatekeeperPort" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.GatekeeperPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.SentDHCPOptionNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.SentDHCPOptionNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACFromClientIDFilter" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACFromClientIDFilter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Location_Name" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Location_Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Location_Name" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.EOMTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.EOMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_ReceivePacketLossRate" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_ReceivePacketLossRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_ReceivePacketLossRate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DNSServers" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DNSServers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IotServerURL" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IotServerURL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IotServerURL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.AvailableInterfaceKey" elementDefinition="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.AvailableInterfaceKey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.RegistrarServer" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.RegistrarServer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.EthernetPriority" elementDefinition="InternetGatewayDevice.UploadDiagnostics.EthernetPriority" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.DefaultEthernetPriorityMark" elementDefinition="InternetGatewayDevice.QueueManagement.DefaultEthernetPriorityMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.SetupLockedState" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.SetupLockedState" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_RouterAdvertisement.MinRtrAdvInterval" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_RouterAdvertisement.MinRtrAdvInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_RouterAdvertisement.MinRtrAdvInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.ISPPhoneNumber" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.ISPPhoneNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_AverageRoundTripDelay" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_AverageRoundTripDelay" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_AverageRoundTripDelay" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SftpPassword" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SftpPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SftpPassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.DigitMap" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.DigitMap" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.WarnDisconnectDelay" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.WarnDisconnectDelay" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.ACSUsername" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.ACSUsername" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.ACSUsername" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNMaximumKeepAlivePeriod" elementDefinition="InternetGatewayDevice.ManagementServer.STUNMaximumKeepAlivePeriod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.TelnetEnable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.TelnetEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.TelnetEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Analytics.Command" elementDefinition="InternetGatewayDevice.X_ALU-COM_Analytics.Command" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Analytics.Command" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.PhysicalMedium.{i}.Name" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.PhysicalMedium.{i}.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.EthernetPriorityMark" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.EthernetPriorityMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.RouteProtocolRx" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.RouteProtocolRx" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_OverSizePacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_OverSizePacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_OverSizePacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.Interface" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UrlFilterCfg.ExcludeMode" elementDefinition="InternetGatewayDevice.X_ALU-COM_UrlFilterCfg.ExcludeMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UrlFilterCfg.ExcludeMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.MiddlewareVersion" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.MiddlewareVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.MiddlewareVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.Timeout" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.Timeout" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Status" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Status" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PreSharedKey.{i}.PreSharedKey" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PreSharedKey.{i}.PreSharedKey" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.TemperatureStatus.TemperatureSensor.{i}.Name" elementDefinition="InternetGatewayDevice.DeviceInfo.TemperatureStatus.TemperatureSensor.{i}.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.FirstSpecialRule" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.FirstSpecialRule" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.FirstSpecialRule" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.BandwidthEgress" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.BandwidthEgress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.BandwidthEgress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.DeviceType" elementDefinition="InternetGatewayDevice.DeviceInfo.DeviceType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.DeviceType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.UAMServer" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.UAMServer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.UAMServer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.PeriodicInformTime" elementDefinition="InternetGatewayDevice.ManagementServer.PeriodicInformTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.MinimumResponseTime" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.MinimumResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.PONLOSSwitchWait" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.PONLOSSwitchWait" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.PONLOSSwitchWait" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FtpUserName" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FtpUserName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FtpUserName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.IPv6DNSConfigType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.IPv6DNSConfigType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.IPv6DNSConfigType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.LteRsrp" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.LteRsrp" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.LteRsrp" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnectionRequestPassword" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnectionRequestPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnectionRequestPassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicEncryptionModes" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicEncryptionModes" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Resistance_Ring_Ground-Kohm" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Resistance_Ring_Ground-Kohm" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Resistance_Ring_Ground-Kohm" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnReqXMPPConnection" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnReqXMPPConnection" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnReqXMPPConnection" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.Fclass" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.Fclass" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACFromVendorClassIDFilterExclude" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACFromVendorClassIDFilterExclude" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.PayloadType" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.PayloadType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.ReminderCrontab" elementDefinition="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.ReminderCrontab" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.ReminderCrontab" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.X_ALU-COM_PortStatus" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.X_ALU-COM_PortStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.X_ALU-COM_PortStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.GRE.X_ALU-COM_Opt82CircuitID" elementDefinition="InternetGatewayDevice.GRE.X_ALU-COM_Opt82CircuitID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.GRE.X_ALU-COM_Opt82CircuitID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.EventSubscribe.{i}.ExpireTime" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.EventSubscribe.{i}.ExpireTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.BulkData.Profile.{i}.HTTP.{i}.Password" elementDefinition="InternetGatewayDevice.BulkData.Profile.{i}.HTTP.{i}.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.BulkData.Profile.{i}.HTTP.{i}.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.EthernetPriority" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.EthernetPriority" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalBytesReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalBytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SambaWorkGroup" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SambaWorkGroup" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SambaWorkGroup" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iEncryptionModes" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iEncryptionModes" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.IllegalCharPrompt" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.IllegalCharPrompt" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.IllegalCharPrompt" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.DiagnosticsState" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.DiagnosticsState" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.Hosts.HostNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.Hosts.HostNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_RouterAdvertisement.AdvManagedFlag" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_RouterAdvertisement.AdvManagedFlag" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_RouterAdvertisement.AdvManagedFlag" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.SubnetMask" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.SubnetMask" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnknownProtoPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnknownProtoPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UrlFilterCfg.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_UrlFilterCfg.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UrlFilterCfg.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.UplinkType" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.UplinkType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.UplinkType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_ResistiveFaults_TestResult" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_ResistiveFaults_TestResult" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_ResistiveFaults_TestResult" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.ConferenceCallingSessionCount" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.ConferenceCallingSessionCount" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_SessionDirection" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_SessionDirection" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_SessionDirection" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.MessageWaiting" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.MessageWaiting" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.KeyPassphrase" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.KeyPassphrase" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_Authentication.Account.ModifyPassword" elementDefinition="InternetGatewayDevice.X_Authentication.Account.ModifyPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.Account.ModifyPassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.HOTRESET.WEBHotreset" elementDefinition="InternetGatewayDevice.HOTRESET.WEBHotreset" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.HOTRESET.WEBHotreset" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.PassthroughMACAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.PassthroughMACAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.DynamicWhitelist" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.DynamicWhitelist" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.DynamicWhitelist" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_DHCPv6Server.MaxAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_DHCPv6Server.MaxAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_DHCPv6Server.MaxAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.CWMPRetryMinimumWaitInterval" elementDefinition="InternetGatewayDevice.ManagementServer.CWMPRetryMinimumWaitInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.RepeatDialEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.RepeatDialEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ALU-COM_Option60Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ALU-COM_Option60Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ALU-COM_Option60Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.AllowedMACAddresses" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.AllowedMACAddresses" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.UAMSecret" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.UAMSecret" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.UAMSecret" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.HOTRESET.WiFiHotreset" elementDefinition="InternetGatewayDevice.HOTRESET.WiFiHotreset" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.HOTRESET.WiFiHotreset" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NWCC.L1Server.Password" elementDefinition="InternetGatewayDevice.X_ALU-COM_NWCC.L1Server.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NWCC.L1Server.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.TelnetPort" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.TelnetPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.TelnetPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.VoiceProcessing.X_ALU-COM_POTSHoldoverTimer" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.VoiceProcessing.X_ALU-COM_POTSHoldoverTimer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.VoiceProcessing.X_ALU-COM_POTSHoldoverTimer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_DhcpcWaitTime" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_DhcpcWaitTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_DhcpcWaitTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetErrorsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetErrorsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_ReversePower.Ilim" elementDefinition="InternetGatewayDevice.X_ALU-COM_ReversePower.Ilim" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_ReversePower.Ilim" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.EchoPlusSupported" elementDefinition="InternetGatewayDevice.UDPEchoConfig.EchoPlusSupported" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.RouteHopsNumberOfEntries" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.RouteHopsNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.MaxQueues" elementDefinition="InternetGatewayDevice.QueueManagement.MaxQueues" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.BridgeNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.BridgeNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU_OntOpticalParam.Status" elementDefinition="InternetGatewayDevice.X_ALU_OntOpticalParam.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU_OntOpticalParam.Status" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU_COM_IPv6NAEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU_COM_IPv6NAEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU_COM_IPv6NAEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.X_ALU_COM_XMPP_Enable" elementDefinition="InternetGatewayDevice.ManagementServer.X_ALU_COM_XMPP_Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.X_ALU_COM_XMPP_Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.ProtocolVersion" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.ProtocolVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.ProtocolVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.FaxT38.Enable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.FaxT38.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WMMEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WMMEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AllowedMACAddresses" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AllowedMACAddresses" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AllowedMACAddresses" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.DownloadDiagnosticMaxConnections" elementDefinition="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.DownloadDiagnosticMaxConnections" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.DownloadDiagnosticMaxConnections" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.TrackFailRecoverDelay" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.TrackFailRecoverDelay" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.TrackFailRecoverDelay" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.AlarmReportingMechanism" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.AlarmReportingMechanism" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.AlarmReportingMechanism" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_VirtualIfCfg_MaxAssoc" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_VirtualIfCfg_MaxAssoc" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_VirtualIfCfg_MaxAssoc" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TCPOpenResponseTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TCPOpenResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolumeNumberOfEntries" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolumeNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.NetMonitorDiagnostics.Hostname" elementDefinition="InternetGatewayDevice.NetMonitorDiagnostics.Hostname" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.NetMonitorDiagnostics.Hostname" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.FailureCount" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.FailureCount" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.RTCP.TxRepeatInterval" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.RTCP.TxRepeatInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_RGCounters.DomainName" elementDefinition="InternetGatewayDevice.X_ALU-COM_RGCounters.DomainName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_RGCounters.DomainName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_ReversePower.IntervalDetect" elementDefinition="InternetGatewayDevice.X_ALU-COM_ReversePower.IntervalDetect" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_ReversePower.IntervalDetect" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.MemoryStatus.Total" elementDefinition="InternetGatewayDevice.DeviceInfo.MemoryStatus.Total" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.Enable1731" elementDefinition="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.Enable1731" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.Enable1731" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EtsiPse.FirmwareVersion" elementDefinition="InternetGatewayDevice.X_ALU-COM_EtsiPse.FirmwareVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EtsiPse.FirmwareVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Lease" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Lease" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Lease" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.BOMTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.BOMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.RingVolumeStatus" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.RingVolumeStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MACAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MACAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestMeasurementInterval" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestMeasurementInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestMeasurementInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.AccessType" elementDefinition="InternetGatewayDevice.DeviceInfo.AccessType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.AccessType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.IMSI" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.IMSI" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.IMSI" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Manufacturer" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Manufacturer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Manufacturer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ShapingRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ShapingRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.OperatorSupportLink" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.OperatorSupportLink" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.OperatorSupportLink" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTStatus" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_CRCErrorSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_CRCErrorSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_CRCErrorSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.DSCPMark" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.DSCPMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.UploadDiagnostics.DSCP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_LogServerCfg.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_LogServerCfg.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_LogServerCfg.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.DeviceLog" elementDefinition="InternetGatewayDevice.DeviceInfo.DeviceLog" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.InterimInterval" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.InterimInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.InterimInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.SendRSIPImmediately" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.SendRSIPImmediately" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.SIP.SIPEventSubscribeNumberOfElements" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.SIP.SIPEventSubscribeNumberOfElements" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.Interface" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WMMSupported" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WMMSupported" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.NetInfo.HostName" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.NetInfo.HostName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.BulkData.Profile.{i}.X_ALU-COM_OltOamIpAddr" elementDefinition="InternetGatewayDevice.BulkData.Profile.{i}.X_ALU-COM_OltOamIpAddr" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.BulkData.Profile.{i}.X_ALU-COM_OltOamIpAddr" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ShapingBurstSize" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ShapingBurstSize" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.FirstSpecialPrompt" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.FirstSpecialPrompt" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.FirstSpecialPrompt" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.VLANIDMark" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.VLANIDMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.PeriodicInformInterval" elementDefinition="InternetGatewayDevice.ManagementServer.PeriodicInformInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.PhysicalReference" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.PhysicalReference" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Interface" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Interface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSentUnderFullLoading" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSentUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSentUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Analytics.DeviceDataCollectionEnable" elementDefinition="InternetGatewayDevice.X_ALU-COM_Analytics.DeviceDataCollectionEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Analytics.DeviceDataCollectionEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.DownloadTransports" elementDefinition="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.DownloadTransports" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPConditionalPoolNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPConditionalPoolNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.X_ALU-COM_IncomingTotalCallTime" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.X_ALU-COM_IncomingTotalCallTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.X_ALU-COM_IncomingTotalCallTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SourceIPAddress" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SourceIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SourceIPAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.Channel" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.Channel" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.Channel" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.ServerIp" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.ServerIp" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.ServerIp" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.AdditionalSoftwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.AdditionalSoftwareVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AuthenticationServiceMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AuthenticationServiceMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.ClassificationNumberOfEntries" elementDefinition="InternetGatewayDevice.QueueManagement.ClassificationNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.TelephoneEventPayloadType" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.TelephoneEventPayloadType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.SuccessCount" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.SuccessCount" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.DataBlockSize" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.DataBlockSize" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_ForeignEMF_TestResult" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_ForeignEMF_TestResult" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_ForeignEMF_TestResult" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.Protocol" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.Protocol" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.Protocol" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UserInterface.X_ALU-COM_CarrierLocking.X_ALU-COM_LockingStatus" elementDefinition="InternetGatewayDevice.UserInterface.X_ALU-COM_CarrierLocking.X_ALU-COM_LockingStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UserInterface.X_ALU-COM_CarrierLocking.X_ALU-COM_LockingStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANConfigSecurity.ConfigPassword" elementDefinition="InternetGatewayDevice.LANConfigSecurity.ConfigPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.DiscardPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.DiscardPacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UPnP.Discovery.DeviceNumberOfEntries" elementDefinition="InternetGatewayDevice.UPnP.Discovery.DeviceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnReqAllowedJabberIDs" elementDefinition="InternetGatewayDevice.ManagementServer.ConnReqAllowedJabberIDs" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.HardwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.HardwareVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_CT-COM_WANGponLinkConfig.VLANIDMark" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_CT-COM_WANGponLinkConfig.VLANIDMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_CT-COM_WANGponLinkConfig.VLANIDMark" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAP" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AppCfg.PortFilterCfg.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_AppCfg.PortFilterCfg.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AppCfg.PortFilterCfg.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.LocalTimeZoneName" elementDefinition="InternetGatewayDevice.Time.LocalTimeZoneName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACFromClientIDFilterExclude" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACFromClientIDFilterExclude" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_VoiceNetworkMode" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_VoiceNetworkMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_VoiceNetworkMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Uptime" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Uptime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.Codecs.{i}.EntryID" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.Codecs.{i}.EntryID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.X_ALU-COM_Option82Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.X_ALU-COM_Option82Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.X_ALU-COM_Option82Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Security.CfgIntegrityCheck.DeltaConfigurationFileCheckResult" elementDefinition="InternetGatewayDevice.Security.CfgIntegrityCheck.DeltaConfigurationFileCheckResult" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Security.CfgIntegrityCheck.DeltaConfigurationFileCheckResult" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.MaxSessionsPerLine" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.MaxSessionsPerLine" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.ISPNewsServer" elementDefinition="InternetGatewayDevice.UserInterface.ISPNewsServer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Stats.BytesReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Stats.BytesReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Stats.BytesReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.VLANIDFilter" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.VLANIDFilter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UploadDiagnosticsMaxConnections" elementDefinition="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UploadDiagnosticsMaxConnections" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UploadDiagnosticsMaxConnections" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.LocationDescription" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.LocationDescription" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Alias" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Alias" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Alias" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.Timeout" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.Timeout" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Clientcert" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Clientcert" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Clientcert" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.NetMonitorDiagnostics.Type" elementDefinition="InternetGatewayDevice.NetMonitorDiagnostics.Type" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.NetMonitorDiagnostics.Type" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.PrefixMinNumberOfDigits" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.PrefixMinNumberOfDigits" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTConfigRestoreStatus" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTConfigRestoreStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTConfigRestoreStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ASB_COM_DmzIpHostCfg.ExcludeIPAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ASB_COM_DmzIpHostCfg.ExcludeIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ASB_COM_DmzIpHostCfg.ExcludeIPAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.TimeToLive" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.TimeToLive" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AppCfg.X_LinkCfg.X_LinkType" elementDefinition="InternetGatewayDevice.X_ALU-COM_AppCfg.X_LinkCfg.X_LinkType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AppCfg.X_LinkCfg.X_LinkType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.ManagementIdleDisconnectTime" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.ManagementIdleDisconnectTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.ManagementIdleDisconnectTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnicastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.UnicastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.ReceiveInterarrivalJitter" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.ReceiveInterarrivalJitter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPowerSupported" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPowerSupported" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Enable" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.JVMVersion" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.JVMVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.JVMVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.PossibleConnectionTypes" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.PossibleConnectionTypes" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBroadcastPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBroadcastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicDataTransmitRates" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BasicDataTransmitRates" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SpeedTest.Mode" elementDefinition="InternetGatewayDevice.X_ALU-COM_SpeedTest.Mode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SpeedTest.Mode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.Codecs.{i}.PacketizationPeriod" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.Codecs.{i}.PacketizationPeriod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_Authentication.WebAccount.Password" elementDefinition="InternetGatewayDevice.X_Authentication.WebAccount.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.WebAccount.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.UnknownProtoPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.UnknownProtoPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.UnknownProtoPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceivedUnderFullLoading" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceivedUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceivedUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.AliasBasedAddressing" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.AliasBasedAddressing" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.AliasBasedAddressing" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.X_ALU-COM_OutgoingTotalCallTime" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.X_ALU-COM_OutgoingTotalCallTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.X_ALU-COM_OutgoingTotalCallTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_LED.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_LED.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_LED.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Connection.{i}.ActiveConnectionDeviceContainer" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Connection.{i}.ActiveConnectionDeviceContainer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.MGCP.Extensions" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.MGCP.Extensions" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MiniLenRule" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MiniLenRule" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MiniLenRule" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnReqJabberID" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnReqJabberID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnReqJabberID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AutoPortBind.X_ALU-COM_AutoPortBindMode" elementDefinition="InternetGatewayDevice.X_ALU-COM_AutoPortBind.X_ALU-COM_AutoPortBindMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AutoPortBind.X_ALU-COM_AutoPortBindMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_SwMgnt.X_ALU-COM_Client_Auth_Key" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_SwMgnt.X_ALU-COM_Client_Auth_Key" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_SwMgnt.X_ALU-COM_Client_Auth_Key" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_CRCErrorReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_CRCErrorReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_CRCErrorReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.RSIPAvailable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.RSIPAvailable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestDuration" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestDuration" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestDuration" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_Authentication.HelpInfo" elementDefinition="InternetGatewayDevice.X_Authentication.HelpInfo" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.HelpInfo" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.InternetPvc" elementDefinition="InternetGatewayDevice.ManagementServer.InternetPvc" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.InternetPvc" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.X_ALU-COM_PolicyNumberOfEntries" elementDefinition="InternetGatewayDevice.QueueManagement.X_ALU-COM_PolicyNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.QueueManagement.X_ALU-COM_PolicyNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.DefaultQueue" elementDefinition="InternetGatewayDevice.QueueManagement.DefaultQueue" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_CallHoldProvision" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_CallHoldProvision" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_CallHoldProvision" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.Secret" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.Secret" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.Secret" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterBridgeReference" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterBridgeReference" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.IndividualPacketResultNumberOfEntries" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.IndividualPacketResultNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.IndividualPacketResultNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Ookla.ThreadCount" elementDefinition="InternetGatewayDevice.X_ALU-COM_Ookla.ThreadCount" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Ookla.ThreadCount" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_DelAddVoice" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_DelAddVoice" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_DelAddVoice" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.InsecureOOBAccessEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.InsecureOOBAccessEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.SftpDisabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.SftpDisabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.SftpDisabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.CLIPrompt" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.CLIPrompt" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.CLIPrompt" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.RTCP.LocalCName" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.RTCP.LocalCName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.EnableCWMP" elementDefinition="InternetGatewayDevice.ManagementServer.EnableCWMP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Model" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Model" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Model" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.MulticastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.MulticastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.MaxFlowEntries" elementDefinition="InternetGatewayDevice.QueueManagement.MaxFlowEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.WarmlineDelayTimer" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.WarmlineDelayTimer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.WarmlineDelayTimer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_BaseCfg_GlobalMaxAssoc" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_BaseCfg_GlobalMaxAssoc" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_BaseCfg_GlobalMaxAssoc" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.TelnetPassword" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.TelnetPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.TelnetPassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_ALU-COM_WANUSBDongleLinkConfig.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_ALU-COM_WANUSBDongleLinkConfig.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_ALU-COM_WANUSBDongleLinkConfig.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ALU-COM_Option82Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ALU-COM_Option82Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ALU-COM_Option82Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallForwardUnconditionalNumber" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallForwardUnconditionalNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UPnP.Description.DeviceDescriptionNumberOfEntries" elementDefinition="InternetGatewayDevice.UPnP.Description.DeviceDescriptionNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.NSLookupDiagnostics.DNSServer" elementDefinition="InternetGatewayDevice.NSLookupDiagnostics.DNSServer" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.SoftwareModules.ExecEnv.{i}.ProcessorRefList" elementDefinition="InternetGatewayDevice.SoftwareModules.ExecEnv.{i}.ProcessorRefList" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Folder.{i}.Name" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Folder.{i}.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceConfig.ConfigFile" elementDefinition="InternetGatewayDevice.DeviceConfig.ConfigFile" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Basic_Location_Policy_Rules" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Basic_Location_Policy_Rules" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Basic_Location_Policy_Rules" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.CAcert" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.CAcert" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.CAcert" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.SNR" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.SNR" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.SNR" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SpeedTest.Upload" elementDefinition="InternetGatewayDevice.X_ALU-COM_SpeedTest.Upload" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SpeedTest.Upload" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.FailureCount" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.FailureCount" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.FailureCount" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.Extensions" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.Extensions" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.DTMFRedundancy" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.DTMFRedundancy" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsReceivedBroadcast" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsReceivedBroadcast" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsReceivedBroadcast" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_BulkData.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_BulkData.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_BulkData.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.FaxT38" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.FaxT38" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.InterfaceID" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.InterfaceID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.ProxyServerTransport" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.ProxyServerTransport" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfoMaxEntries" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfoMaxEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SessionFailureReason" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SessionFailureReason" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SessionFailureReason" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.ProtocolVersion" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.ProtocolVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.ProtocolVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU_OntOpticalParam.RXPowerLower" elementDefinition="InternetGatewayDevice.X_ALU_OntOpticalParam.RXPowerLower" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU_OntOpticalParam.RXPowerLower" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_GPON.TransceiverNumberOfEntries" elementDefinition="InternetGatewayDevice.X_ALU-COM_GPON.TransceiverNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_GPON.TransceiverNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.LocalTimeZone" elementDefinition="InternetGatewayDevice.Time.LocalTimeZone" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.DownloadDiagnosticsMaxIncrementalResult" elementDefinition="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.DownloadDiagnosticsMaxIncrementalResult" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.DownloadDiagnosticsMaxIncrementalResult" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.PacketsSent" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.PacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.PacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetErrorsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetErrorsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.RemoteMepId" elementDefinition="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.RemoteMepId" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.RemoteMepId" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallerIDNameEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallerIDNameEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_Authentication.Account.Priority" elementDefinition="InternetGatewayDevice.X_Authentication.Account.Priority" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.Account.Priority" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.NSLookupDiagnostics.NumberOfRepetitions" elementDefinition="InternetGatewayDevice.NSLookupDiagnostics.NumberOfRepetitions" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.SIPResponseMapNumberOfElements" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.SIPResponseMapNumberOfElements" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MESH_WDSHideSSID.SSID5G" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MESH_WDSHideSSID.SSID5G" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MESH_WDSHideSSID.SSID5G" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_Op50ReqIp" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_Op50ReqIp" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_Op50ReqIp" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.UpTime" elementDefinition="InternetGatewayDevice.DeviceInfo.UpTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceivedUnderFullLoading" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceivedUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceivedUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU_EnterpriseNumb" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU_EnterpriseNumb" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU_EnterpriseNumb" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ExternalIPAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ExternalIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.Host" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.Host" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Status" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UPnP.Device.Capabilities.UPnPArchitectureMinorVer" elementDefinition="InternetGatewayDevice.UPnP.Device.Capabilities.UPnPArchitectureMinorVer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Ringer.PatternNumberOfEntries" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Ringer.PatternNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.MarkingNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.MarkingNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.GRE.X_ALU-COM_CurrentTunnelMode" elementDefinition="InternetGatewayDevice.GRE.X_ALU-COM_CurrentTunnelMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.GRE.X_ALU-COM_CurrentTunnelMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UserInterface.UpgradeAvailable" elementDefinition="InternetGatewayDevice.UserInterface.UpgradeAvailable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.SpecVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.SpecVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.DownstreamMaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.DownstreamMaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.DownstreamMaxBitRate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.VoiceProcessing.ReceiveGain" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.VoiceProcessing.ReceiveGain" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.MaxBridgeEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.MaxBridgeEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.X_ALU-COM_MaxClassifierEntries" elementDefinition="InternetGatewayDevice.QueueManagement.X_ALU-COM_MaxClassifierEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.QueueManagement.X_ALU-COM_MaxClassifierEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.DebugDyPass.Enable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.DebugDyPass.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.DebugDyPass.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.TotalCallTime" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.TotalCallTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.RingMuteStatus" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.RingMuteStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANWLANConfigurationNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANWLANConfigurationNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.WorkMode" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.WorkMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.WorkMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SignalingProtocol" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SignalingProtocol" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_DeniedMACAddresses" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_DeniedMACAddresses" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_DeniedMACAddresses" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigMethodsEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigMethodsEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.Radio" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.Radio" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.Radio" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.Interface" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.Interface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.MaxLoggedinUsers" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.MaxLoggedinUsers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.MaxLoggedinUsers" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.VendorConfigFile.{i}.Date" elementDefinition="InternetGatewayDevice.DeviceInfo.VendorConfigFile.{i}.Date" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ConnectionTrigger" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ConnectionTrigger" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.LimitAccount_ONTUSER" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.LimitAccount_ONTUSER" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.LimitAccount_ONTUSER" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TestBytesSentUnderFullLoading" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TestBytesSentUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TestBytesSentUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.BytesResponded" elementDefinition="InternetGatewayDevice.UDPEchoConfig.BytesResponded" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.FolderNumberOfEntries" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.FolderNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ModemFirmwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.ModemFirmwareVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ALU-COM_InterDigitTimer" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ALU-COM_InterDigitTimer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ALU-COM_InterDigitTimer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ButtonMap.NumberOfButtons" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ButtonMap.NumberOfButtons" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.PolicerNumberOfEntries" elementDefinition="InternetGatewayDevice.QueueManagement.PolicerNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Alias" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Alias" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.DigitMap" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.DigitMap" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_LogServerCfg.X_ALU-COM_Polling_Time" elementDefinition="InternetGatewayDevice.X_ALU-COM_LogServerCfg.X_ALU-COM_Polling_Time" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_LogServerCfg.X_ALU-COM_Polling_Time" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.EthernetPriorityMark" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.EthernetPriorityMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.MulticastPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.MulticastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.MulticastPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.MaxPolicerEntries" elementDefinition="InternetGatewayDevice.QueueManagement.MaxPolicerEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_PacketsSent" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_PacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_PacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.CpuInfo.CPUTemp" elementDefinition="InternetGatewayDevice.DeviceInfo.CpuInfo.CPUTemp" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.CpuInfo.CPUTemp" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsReceivedMulticast" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsReceivedMulticast" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsReceivedMulticast" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadURL" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DownloadURL" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.IPVer" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.IPVer" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.IPPingDiagnostics.IPVer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.X_ALU-COM_DHCPRelay" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.X_ALU-COM_DHCPRelay" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.X_ALU-COM_DHCPRelay" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PreSharedKey.{i}.DefaultPreSharedKey" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PreSharedKey.{i}.DefaultPreSharedKey" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PreSharedKey.{i}.DefaultPreSharedKey" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Enable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPower" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TransmitPower" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_FarEndInterarrivalJitter" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_FarEndInterarrivalJitter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_FarEndInterarrivalJitter" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetMulticastPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetMulticastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_ReversePower.IntervalCheck" elementDefinition="InternetGatewayDevice.X_ALU-COM_ReversePower.IntervalCheck" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_ReversePower.IntervalCheck" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.Identifier" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.Identifier" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.Identifier" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.Domain" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.Domain" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.WANAccessProvider" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.WANAccessProvider" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.MdId" elementDefinition="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.MdId" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.MdId" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.RegisterRetryInterval" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.RegisterRetryInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.UDPEchoDiagnosticsMaxResults" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.UDPEchoDiagnosticsMaxResults" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.UDPEchoDiagnosticsMaxResults" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Region" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Region" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.ZwaveIntfStatus" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.ZwaveIntfStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.ZwaveIntfStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTStatusDesc" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTStatusDesc" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTStatusDesc" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.NumberingPlan" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.NumberingPlan" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_CT-COM_WANGponLinkConfig.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_CT-COM_WANGponLinkConfig.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_CT-COM_WANGponLinkConfig.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.EnabledOptions" elementDefinition="InternetGatewayDevice.DeviceInfo.EnabledOptions" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AppCfg.OperatorPlugins.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_AppCfg.OperatorPlugins.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AppCfg.OperatorPlugins.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SambaPassword" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SambaPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SambaPassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.PatternBasedToneGeneration" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.PatternBasedToneGeneration" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.PINStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.PINStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.PINStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPServer" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPServer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPServer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.SshTrusted" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.SshTrusted" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.SshTrusted" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.ConnectionStatus" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.ConnectionStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.ConnectionStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SpeedTest.ConfigTR143.{i}.Host" elementDefinition="InternetGatewayDevice.X_ALU-COM_SpeedTest.ConfigTR143.{i}.Host" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SpeedTest.ConfigTR143.{i}.Host" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.ReservedAddresses" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.ReservedAddresses" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.VoiceRedundancy" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.VoiceRedundancy" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.UDPServerPort" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.UDPServerPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.UDPServerPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_ALU-COM_ChannelUtilization" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_ALU-COM_ChannelUtilization" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_ALU-COM_ChannelUtilization" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SftpUserName" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SftpUserName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SftpUserName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.DataCompression" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.DataCompression" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.SupportLink" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.SupportLink" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.SupportLink" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Security.CfgIntegrityCheck.UnsignedCfgFileSupported" elementDefinition="InternetGatewayDevice.Security.CfgIntegrityCheck.UnsignedCfgFileSupported" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Security.CfgIntegrityCheck.UnsignedCfgFileSupported" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SupportedStandards" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SupportedStandards" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SupportedStandards" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.SoftwareModules.DeploymentUnitNumberOfEntries" elementDefinition="InternetGatewayDevice.SoftwareModules.DeploymentUnitNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Security.CfgIntegrityCheck.PreConfigurationFileCheckResult" elementDefinition="InternetGatewayDevice.Security.CfgIntegrityCheck.PreConfigurationFileCheckResult" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Security.CfgIntegrityCheck.PreConfigurationFileCheckResult" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPSSID5Interface" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPSSID5Interface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPSSID5Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.Regions" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.Regions" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.PacketsSent" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.PacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallWaitingStatus" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallWaitingStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.LocalUDPPort" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.LocalUDPPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelSupported" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelSupported" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelSupported" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.MaxAppEntries" elementDefinition="InternetGatewayDevice.QueueManagement.MaxAppEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.NumberOfRepetitions" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.NumberOfRepetitions" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.NumberOfRepetitions" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestMeasurementInterval" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestMeasurementInterval" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestMeasurementInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FtpRemoteAccessEnable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FtpRemoteAccessEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FtpRemoteAccessEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_RGCounters.Latency" elementDefinition="InternetGatewayDevice.X_ALU-COM_RGCounters.Latency" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_RGCounters.Latency" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.User" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.User" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_AverageFarEndInterarrivalJitter" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_AverageFarEndInterarrivalJitter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_AverageFarEndInterarrivalJitter" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.LastConnectionError" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.LastConnectionError" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FtpPassword" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FtpPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FtpPassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.TelnetDisabled" elementDefinition="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.TelnetDisabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.TelnetDisabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.Overruns" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.Overruns" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.FaxT38.HighSpeedRedundancy" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.FaxT38.HighSpeedRedundancy" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SpeedTest.ConfigTR143.{i}.DownloadURL" elementDefinition="InternetGatewayDevice.X_ALU-COM_SpeedTest.ConfigTR143.{i}.DownloadURL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SpeedTest.ConfigTR143.{i}.DownloadURL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.HttpsTrusted" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.HttpsTrusted" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.HttpsTrusted" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.MACAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.MACAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_GEUpLinkEnable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_GEUpLinkEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_GEUpLinkEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.FTPCapable" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.FTPCapable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.FTPCapable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.DeviceName" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.DeviceName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.RTCP.Enable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.RTCP.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingBridgeReference" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingBridgeReference" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.PPPOptfile" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.PPPOptfile" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.PPPOptfile" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.UnicastPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.UnicastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.UnicastPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_WOLAN.Enable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_WOLAN.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_WOLAN.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.RingGeneration" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.RingGeneration" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Status" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.MSISDN" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.MSISDN" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.MSISDN" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSent" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ALU_COM_NACKSendSwitch" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ALU_COM_NACKSendSwitch" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ALU_COM_NACKSendSwitch" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.Stats.PacketsReceived" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.Stats.PacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.Stats.PacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ButtonMap.Button.{i}.FacilityActionArgument" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ButtonMap.Button.{i}.FacilityActionArgument" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.L2TPHelloDelay" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.L2TPHelloDelay" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.L2TPHelloDelay" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UserInterface.ExamplePassword" elementDefinition="InternetGatewayDevice.UserInterface.ExamplePassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnectionRequestPassword" elementDefinition="InternetGatewayDevice.ManagementServer.ConnectionRequestPassword" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer3Forwarding.ForwardNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer3Forwarding.ForwardNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.Username" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.Username" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.Username" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.BackupUplink" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.BackupUplink" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.BackupUplink" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.ReceiveSilenceSuppression" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.ReceiveSilenceSuppression" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NWCC.L2Server.URL" elementDefinition="InternetGatewayDevice.X_ALU-COM_NWCC.L2Server.URL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NWCC.L2Server.URL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.InstanceMode" elementDefinition="InternetGatewayDevice.ManagementServer.InstanceMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.IcmpEchoReqDisabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.IcmpEchoReqDisabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.IcmpEchoReqDisabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerT1" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerT1" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_OverSizePacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_OverSizePacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_OverSizePacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.MGCP.LineName" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.MGCP.LineName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.OutgoingCallsConnected" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.OutgoingCallsConnected" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IoTAppUser.IoTAppAccount.{i}.Password" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IoTAppUser.IoTAppAccount.{i}.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IoTAppUser.IoTAppAccount.{i}.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerT2" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerT2" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NWCC.RemoteMobileAccess.URL" elementDefinition="InternetGatewayDevice.X_ALU-COM_NWCC.RemoteMobileAccess.URL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NWCC.RemoteMobileAccess.URL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPacketsReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerT4" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerT4" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TotalBytesSentUnderFullLoading" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TotalBytesSentUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TotalBytesSentUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_SwMgnt.X_ALU-COM_Polling_Time" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_SwMgnt.X_ALU-COM_Polling_Time" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_SwMgnt.X_ALU-COM_Polling_Time" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenRequestTime" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TCPOpenRequestTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.Category" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.Category" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.Category" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SpeedTest.ISP" elementDefinition="InternetGatewayDevice.X_ALU-COM_SpeedTest.ISP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SpeedTest.ISP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.Version" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.Version" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.ReInviteExpires" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.ReInviteExpires" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.InviteExpires" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.InviteExpires" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.STUNServer" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.STUNServer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SupportedStandards" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SupportedStandards" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SupportedStandards" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.InterfaceType" elementDefinition="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.InterfaceType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.PlusVTRCommandSupported" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.PlusVTRCommandSupported" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SessionDuration" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SessionDuration" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SessionDuration" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.MaxFilterEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.MaxFilterEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.UsedSpace" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.UsedSpace" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Status" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Status" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.DpdAction" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.DpdAction" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.DpdAction" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.PreferredAccessTechnology" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.PreferredAccessTechnology" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.PreferredAccessTechnology" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU_COM_BandSteering.RSSILowDownSteer" elementDefinition="InternetGatewayDevice.X_ALU_COM_BandSteering.RSSILowDownSteer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU_COM_BandSteering.RSSILowDownSteer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.ICCID" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.ICCID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.ICCID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.VendorConfigFile.{i}.Version" elementDefinition="InternetGatewayDevice.DeviceInfo.VendorConfigFile.{i}.Version" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_BulkData.MinReportingInterval" elementDefinition="InternetGatewayDevice.X_ALU-COM_BulkData.MinReportingInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_BulkData.MinReportingInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.InterCommProtocol" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.InterCommProtocol" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.InterCommProtocol" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AvailableNetworks" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AvailableNetworks" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AvailableNetworks" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_ROH_TestResult" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_ROH_TestResult" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_ROH_TestResult" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.AnonymousCallBlockEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.AnonymousCallBlockEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_BulkData.MaxNumberOfParameterReferences" elementDefinition="InternetGatewayDevice.X_ALU-COM_BulkData.MaxNumberOfParameterReferences" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_BulkData.MaxNumberOfParameterReferences" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.MinimumResponseTime" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.MinimumResponseTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.MinimumResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.MulticastPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.MulticastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.MulticastPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EtsiPse.PseActiveState" elementDefinition="InternetGatewayDevice.X_ALU-COM_EtsiPse.PseActiveState" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EtsiPse.PseActiveState" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceSummary" elementDefinition="InternetGatewayDevice.DeviceSummary" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.NumberOfRepetitions" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.NumberOfRepetitions" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.NumberOfRepetitions" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.ButtonMap" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.ButtonMap" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.StaticWhitelist" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.StaticWhitelist" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.StaticWhitelist" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingStatus" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Name" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_PreventPortScan.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_PreventPortScan.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_PreventPortScan.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.UserAgentDomain" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.UserAgentDomain" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LANIPv6Address.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LANIPv6Address.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LANIPv6Address.{i}.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZwaveCtrl.Reset" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZwaveCtrl.Reset" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZwaveCtrl.Reset" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_NokiaWiFi.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_NokiaWiFi.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_NokiaWiFi.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_HomeIntelligenceServer.Profile.{i}.Username" elementDefinition="InternetGatewayDevice.X_ALU-COM_HomeIntelligenceServer.Profile.{i}.Username" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_HomeIntelligenceServer.Profile.{i}.Username" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.SendersID" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.SendersID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.ResponseMap" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.ResponseMap" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.SIP.EventSubscribe.{i}.AuthPassword" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.SIP.EventSubscribe.{i}.AuthPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_DC_Hazardous_Voltage_thld-Volt" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_DC_Hazardous_Voltage_thld-Volt" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_DC_Hazardous_Voltage_thld-Volt" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.HeartbeatDetectMethod" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.HeartbeatDetectMethod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.HeartbeatDetectMethod" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.RegistrarServerTransport" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.RegistrarServerTransport" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_BeaconInfo.GroupID" elementDefinition="InternetGatewayDevice.X_ALU-COM_BeaconInfo.GroupID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_BeaconInfo.GroupID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MESH_WDSHideSSID.LinkType" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MESH_WDSHideSSID.LinkType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MESH_WDSHideSSID.LinkType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPv6UDPEchoDiagnosticsSupported" elementDefinition="InternetGatewayDevice.IPv6UDPEchoDiagnosticsSupported" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.IPv6UDPEchoDiagnosticsSupported" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Ringer.Event.{i}.RingID" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Ringer.Event.{i}.RingID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.FaxT38.LowSpeedRedundancy" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.FaxT38.LowSpeedRedundancy" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.VoiceProcessing.EchoCancellationTail" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.VoiceProcessing.EchoCancellationTail" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.PurchaseLink" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.PurchaseLink" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.PurchaseLink" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.EncryptionMode" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.EncryptionMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.EncryptionMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.VendorConfigFileNumberOfEntries" elementDefinition="InternetGatewayDevice.DeviceInfo.VendorConfigFileNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.Password" elementDefinition="InternetGatewayDevice.ManagementServer.Password" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.TestSelector" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.TestSelector" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Username" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Username" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Username" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.SupportedNetworkProtocols" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.SupportedNetworkProtocols" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.SupportedNetworkProtocols" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.ModemPassThrough" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.ModemPassThrough" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.HttpDisabled" elementDefinition="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.HttpDisabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.HttpDisabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.NetMonitorDiagnostics.Interface" elementDefinition="InternetGatewayDevice.NetMonitorDiagnostics.Interface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.NetMonitorDiagnostics.Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.CurrentAccessTechnology" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.CurrentAccessTechnology" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.CurrentAccessTechnology" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.LteSignalNoiseRatio" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.LteSignalNoiseRatio" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.LteSignalNoiseRatio" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FtpPort" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FtpPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FtpPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.DSCPCoupled" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.DSCPCoupled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UDPEchoDiagnosticsMaxResults" elementDefinition="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UDPEchoDiagnosticsMaxResults" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UDPEchoDiagnosticsMaxResults" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1DownstreamMaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1DownstreamMaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.OutboundProxyPort" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.OutboundProxyPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.ResetStatistics" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.ResetStatistics" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ALU-COM_Option82SSIDEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ALU-COM_Option82SSIDEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ALU-COM_Option82SSIDEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.H235Authentication" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.H235Authentication" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.NumberOfConnections" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.NumberOfConnections" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.NumberOfConnections" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Channel" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Channel" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_CallTransferProvision" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_CallTransferProvision" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_CallTransferProvision" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.Interface" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.ZigbeeFWVersion" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.ZigbeeFWVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.ZigbeeFWVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ButtonMap.Button.{i}.ButtonName" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ButtonMap.Button.{i}.ButtonName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.VLANIDMark" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.VLANIDMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetDiscardPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetDiscardPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SecurityModeEnabled" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SecurityModeEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SecurityModeEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.DSCPMark" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.DSCPMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.UAPSDEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.UAPSDEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TCPOpenRequestTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TCPOpenRequestTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_UnderSizePacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_UnderSizePacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_UnderSizePacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.MemoryStatus.Free" elementDefinition="InternetGatewayDevice.DeviceInfo.MemoryStatus.Free" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ASB_COM_DmzIpHostCfg.DmzHostDescription" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ASB_COM_DmzIpHostCfg.DmzHostDescription" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ASB_COM_DmzIpHostCfg.DmzHostDescription" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.VLANIDMark" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.VLANIDMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.IncomingCallsReceived" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.IncomingCallsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_NATNumberOfEntries" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_NATNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_NATNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_UpStreamJabbers" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_UpStreamJabbers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_UpStreamJabbers" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Ringer_Load-mREN" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Ringer_Load-mREN" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Ringer_Load-mREN" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallerIDName" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallerIDName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AccessPoint.APN" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AccessPoint.APN" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AccessPoint.APN" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MappHIEURL" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MappHIEURL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MappHIEURL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IoTAppUser.IoTAppAccount.{i}.UserType" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IoTAppUser.IoTAppAccount.{i}.UserType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IoTAppUser.IoTAppAccount.{i}.UserType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotFirmwareInfo.{i}.Description" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotFirmwareInfo.{i}.Description" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotFirmwareInfo.{i}.Description" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNMinimumKeepAlivePeriod" elementDefinition="InternetGatewayDevice.ManagementServer.STUNMinimumKeepAlivePeriod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ModelName" elementDefinition="InternetGatewayDevice.DeviceInfo.ModelName" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Servercert" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Servercert" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Servercert" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceIPAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.STUNEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.STUNEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.NSLookupDiagnostics.Timeout" elementDefinition="InternetGatewayDevice.NSLookupDiagnostics.Timeout" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ASB_COM_EthPort.EthPort.{i}.isTr069Domain" elementDefinition="InternetGatewayDevice.X_ASB_COM_EthPort.EthPort.{i}.isTr069Domain" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ASB_COM_EthPort.EthPort.{i}.isTr069Domain" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_Authentication.TelnetSshAccount.Enable" elementDefinition="InternetGatewayDevice.X_Authentication.TelnetSshAccount.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.TelnetSshAccount.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberOfLines" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberOfLines" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.Role" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.Role" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.DiagnosticsState" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.DiagnosticsState" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_BulkData.Protocols" elementDefinition="InternetGatewayDevice.X_ALU-COM_BulkData.Protocols" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_BulkData.Protocols" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.ICCID" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.ICCID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.ICCID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.X_ALU-COM_SIP_Server_outage" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.X_ALU-COM_SIP_Server_outage" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.X_ALU-COM_SIP_Server_outage" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotFirmwareInfo.{i}.FileName" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotFirmwareInfo.{i}.FileName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotFirmwareInfo.{i}.FileName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.MaxSessions" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.MaxSessions" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.ISPHelpPage" elementDefinition="InternetGatewayDevice.UserInterface.ISPHelpPage" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.IdleDisconnectTime" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.IdleDisconnectTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_Authentication.TelnetSshAccount.Password" elementDefinition="InternetGatewayDevice.X_Authentication.TelnetSshAccount.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.TelnetSshAccount.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.STAPreferredBandEntries" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.STAPreferredBandEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.STAPreferredBandEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.AverageFarEndInterarrivalJitter" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.AverageFarEndInterarrivalJitter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_LogServerCfg.UploadType" elementDefinition="InternetGatewayDevice.X_ALU-COM_LogServerCfg.UploadType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_LogServerCfg.UploadType" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_LogServerCfg.SFTPpassword" elementDefinition="InternetGatewayDevice.X_ALU-COM_LogServerCfg.SFTPpassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_LogServerCfg.SFTPpassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallForwardOnNoAnswerEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallForwardOnNoAnswerEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.UploadDiagnosticsMaxConnections" elementDefinition="InternetGatewayDevice.UploadDiagnostics.UploadDiagnosticsMaxConnections" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.UploadDiagnosticsMaxConnections" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPv4UDPEchoDiagnosticsSupported" elementDefinition="InternetGatewayDevice.IPv4UDPEchoDiagnosticsSupported" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.IPv4UDPEchoDiagnosticsSupported" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsDropped" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsDropped" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsDropped" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.VoiceProcessing.TransmitGain" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.VoiceProcessing.TransmitGain" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.IllegalCharRule" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.IllegalCharRule" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.IllegalCharRule" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_AirTimeFairness" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_AirTimeFairness" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_AirTimeFairness" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.DTMFMethod" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.DTMFMethod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.UpstreamMaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.UpstreamMaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.UpstreamMaxBitRate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Name" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Name" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.MaximumActiveConnections" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.MaximumActiveConnections" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.InboundAuthPassword" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.InboundAuthPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.X_ALU-COM_CodecSelectionRange" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.X_ALU-COM_CodecSelectionRange" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.X_ALU-COM_CodecSelectionRange" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.DataProtocol" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.DataProtocol" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.EnablePerConnectionResults" elementDefinition="InternetGatewayDevice.UploadDiagnostics.EnablePerConnectionResults" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.EnablePerConnectionResults" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU_Op125Enabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU_Op125Enabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU_Op125Enabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.DebugDyPass.PriKey" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.DebugDyPass.PriKey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.DebugDyPass.PriKey" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.PhyPort" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.PhyPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.EthernetPriorityMark" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.EthernetPriorityMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.Noise" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.Noise" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.Noise" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_IGMPCfg.IgmpDsMulticastPriority" elementDefinition="InternetGatewayDevice.X_ALU-COM_IGMPCfg.IgmpDsMulticastPriority" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_IGMPCfg.IgmpDsMulticastPriority" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SpeedTest.ConfigTR143.{i}.TimeDuration" elementDefinition="InternetGatewayDevice.X_ALU-COM_SpeedTest.ConfigTR143.{i}.TimeDuration" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SpeedTest.ConfigTR143.{i}.TimeDuration" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AccessPoint.DialNumber" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AccessPoint.DialNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AccessPoint.DialNumber" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.List.{i}.Codec" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.List.{i}.Codec" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.ProtocolVersion" elementDefinition="InternetGatewayDevice.UploadDiagnostics.ProtocolVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.ProtocolVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZigbeeCtrl.ZigBeeConfigRestoreStatus" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZigbeeCtrl.ZigBeeConfigRestoreStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZigbeeCtrl.ZigBeeConfigRestoreStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.RxRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.RxRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.RxRate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNUsername" elementDefinition="InternetGatewayDevice.ManagementServer.STUNUsername" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MiniClassRule" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MiniClassRule" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MiniClassRule" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Security.SwitchOPID.KeepLablePassword" elementDefinition="InternetGatewayDevice.Security.SwitchOPID.KeepLablePassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Security.SwitchOPID.KeepLablePassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.AdditionalHardwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.AdditionalHardwareVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.RegistrarNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.RegistrarNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_UpStreamJabbers" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_UpStreamJabbers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_UpStreamJabbers" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.InstanceIdentifier" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.InstanceIdentifier" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.InstanceIdentifier" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Keylife" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Keylife" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Keylife" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_UnderSizePacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_UnderSizePacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_UnderSizePacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.LastChange" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.LastChange" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.LastChange" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.SubnetMask" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.SubnetMask" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.Enable" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.NetworkRequested" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.NetworkRequested" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.NetworkRequested" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.DigitMapEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.DigitMapEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddress" elementDefinition="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.FaxPassThrough" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.FaxPassThrough" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.DiscardPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.DiscardPacketsSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.MaximumResponseTime" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.MaximumResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.DTIMPeriod" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.DTIMPeriod" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.DTIMPeriod" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTConfigBackupStatus" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTConfigBackupStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTConfigBackupStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.FastestHost" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.FastestHost" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.FastestHost" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.LastConnectedURL" elementDefinition="InternetGatewayDevice.ManagementServer.LastConnectedURL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.LastConnectedURL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.UserAgentTransport" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.UserAgentTransport" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.RegisterExpires" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.RegisterExpires" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.TextColor" elementDefinition="InternetGatewayDevice.UserInterface.TextColor" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.SoftwareVersion" elementDefinition="InternetGatewayDevice.DeviceInfo.SoftwareVersion" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EtsiPse.ChipTemperature" elementDefinition="InternetGatewayDevice.X_ALU-COM_EtsiPse.ChipTemperature" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EtsiPse.ChipTemperature" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AccessPoint.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AccessPoint.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AccessPoint.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.Status" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.USIM.Status" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.Enable1ag" elementDefinition="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.Enable1ag" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.Enable1ag" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DomainName" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DomainName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.BroadcastPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.BroadcastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.BroadcastPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.IPv6DNSWANConnection" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.IPv6DNSWANConnection" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.IPv6DNSWANConnection" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.UnicastPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.UnicastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.UnicastPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.SourceIPAddress" elementDefinition="InternetGatewayDevice.UDPEchoConfig.SourceIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MaxBitRate" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MaxBitRate" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnicastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnicastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.TrackURL" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.TrackURL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.TrackURL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.ServerDownTime" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.ServerDownTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BroadcastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BroadcastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.PeriodOfFullLoading" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.PeriodOfFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.PeriodOfFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.LocalPort" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.LocalPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_BulkData.MaxNumberOfProfiles" elementDefinition="InternetGatewayDevice.X_ALU-COM_BulkData.MaxNumberOfProfiles" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_BulkData.MaxNumberOfProfiles" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.MulticastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.MulticastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNServerPort" elementDefinition="InternetGatewayDevice.ManagementServer.STUNServerPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.CallAgentPort1" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.CallAgentPort1" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.CallAgentPort2" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.CallAgentPort2" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Analytics.LocalAnalyticsEnable" elementDefinition="InternetGatewayDevice.X_ALU-COM_Analytics.LocalAnalyticsEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Analytics.LocalAnalyticsEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPEncryptionLevel" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPEncryptionLevel" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.X_ALU_DHCPOption125.EnterpriseNumber" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.X_ALU_DHCPOption125.EnterpriseNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.X_ALU_DHCPOption125.EnterpriseNumber" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.HttpTrusted" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.HttpTrusted" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.HttpTrusted" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.TestState" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.TestState" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Alias" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Alias" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Alias" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.FarEndPacketLossRate" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.FarEndPacketLossRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Rekey" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Rekey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Rekey" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Extended_Location_Policy_Rules" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Extended_Location_Policy_Rules" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Extended_Location_Policy_Rules" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsSentBroadcast" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsSentBroadcast" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsSentBroadcast" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IotServerPort" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IotServerPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IotServerPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoRateFallBackEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoRateFallBackEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_RGCounters.Interface" elementDefinition="InternetGatewayDevice.X_ALU-COM_RGCounters.Interface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_RGCounters.Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.EventRaisedTime" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.EventRaisedTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.EventRaisedTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Firewall.LastChange" elementDefinition="InternetGatewayDevice.Firewall.LastChange" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.DisableRemindTemporary" elementDefinition="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.DisableRemindTemporary" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.DisableRemindTemporary" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.X_ALU-COM_EnableServerCertValidation" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.X_ALU-COM_EnableServerCertValidation" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.X_ALU-COM_EnableServerCertValidation" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.WorkRole" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.WorkRole" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.WorkRole" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPSMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPSMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPSMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.Password" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.List.{i}.BitRate" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.List.{i}.BitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_Authentication.Account.Alias" elementDefinition="InternetGatewayDevice.X_Authentication.Account.Alias" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.Account.Alias" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.Enable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.DiagnosticsState" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.DiagnosticsState" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingInterface" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingInterface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.FaxT38.BitRate" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.FaxT38.BitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterKey" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterKey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalIntegrityFailures" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalIntegrityFailures" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.URISchemes" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.URISchemes" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_OverSizePacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_OverSizePacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_OverSizePacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.UDPPort" elementDefinition="InternetGatewayDevice.UDPEchoConfig.UDPPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PeerBSSID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PeerBSSID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACFromClientIDFilterExclude" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACFromClientIDFilterExclude" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_Authentication.Account.UserName" elementDefinition="InternetGatewayDevice.X_Authentication.Account.UserName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.Account.UserName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_PortTriggeringNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_PortTriggeringNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_PortTriggeringNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTGWVersion" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTGWVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTGWVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.PassthroughLease" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.PassthroughLease" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.SecondaryServerIPAddr" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.SecondaryServerIPAddr" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.SecondaryServerIPAddr" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.SupportedDataModelNumberOfEntries" elementDefinition="InternetGatewayDevice.DeviceInfo.SupportedDataModelNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTServerConnStatus" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTServerConnStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTServerConnStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NWCC.L1Server.UserName" elementDefinition="InternetGatewayDevice.X_ALU-COM_NWCC.L1Server.UserName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NWCC.L1Server.UserName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.NetworkingMode" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.NetworkingMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.NetworkingMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.DigitmapMatchPattern" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.DigitmapMatchPattern" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.DigitmapMatchPattern" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_ReversePower.IntervalLimit" elementDefinition="InternetGatewayDevice.X_ALU-COM_ReversePower.IntervalLimit" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_ReversePower.IntervalLimit" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AppCfg.DnsProxyCfg.X_ALU-COM_SecureDNS" elementDefinition="InternetGatewayDevice.X_ALU-COM_AppCfg.DnsProxyCfg.X_ALU-COM_SecureDNS" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AppCfg.DnsProxyCfg.X_ALU-COM_SecureDNS" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.DSCP" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.SoftwareModules.ExecEnv.{i}.Name" elementDefinition="InternetGatewayDevice.SoftwareModules.ExecEnv.{i}.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.MobileDisconnectIdleTime" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.MobileDisconnectIdleTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.MobileDisconnectIdleTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.RegistrarEstablished" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.RegistrarEstablished" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SambaUserName" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SambaUserName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SambaUserName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_UpStreamBwUtilization" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_UpStreamBwUtilization" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_UpStreamBwUtilization" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnectionNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPPPConnectionNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.InterfaceMtu" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.InterfaceMtu" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.InterfaceMtu" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.MaxProfileCount" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.MaxProfileCount" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ASB_COM_DmzIpHostCfg.DmzEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ASB_COM_DmzIpHostCfg.DmzEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ASB_COM_DmzIpHostCfg.DmzEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Name" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Name" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MacAddr" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MacAddr" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.MacAddr" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AppCfg.OperatorPlugins.plugin.{i}.Version" elementDefinition="InternetGatewayDevice.X_ALU-COM_AppCfg.OperatorPlugins.plugin.{i}.Version" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AppCfg.OperatorPlugins.plugin.{i}.Version" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Ookla.ConfigURL" elementDefinition="InternetGatewayDevice.X_ALU-COM_Ookla.ConfigURL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Ookla.ConfigURL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_Authentication.Account.PresetPassword" elementDefinition="InternetGatewayDevice.X_Authentication.Account.PresetPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.Account.PresetPassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.ParameterKey" elementDefinition="InternetGatewayDevice.ManagementServer.ParameterKey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.Timeout" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.Timeout" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.Timeout" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BSSID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BSSID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.CurrentSubMode" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.CurrentSubMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.CurrentSubMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.ISPInfo" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.ISPInfo" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.EthernetPriorityMark" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.EthernetPriorityMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_LogServerCfg.ServerIpAddr" elementDefinition="InternetGatewayDevice.X_ALU-COM_LogServerCfg.ServerIpAddr" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_LogServerCfg.ServerIpAddr" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.PhysicalLinkStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.PhysicalLinkStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.DirectoryNumber" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.DirectoryNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.TrackFrequency" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.TrackFrequency" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.TrackFrequency" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterInterface" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.FilterInterface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.LEDEnable" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.LEDEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.LEDEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.EchoPlusEnabled" elementDefinition="InternetGatewayDevice.UDPEchoConfig.EchoPlusEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.DefaultDSCPMark" elementDefinition="InternetGatewayDevice.QueueManagement.DefaultDSCPMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.Mode" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.Mode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.Mode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.DiscardPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.DiscardPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.DiscardPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SessionSuccessful" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SessionSuccessful" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SessionSuccessful" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.ConnectionTime" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.ConnectionTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.ConnectionTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.DestinationIPAddress" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.DestinationIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.DestinationIPAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.MACAddressOverride" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.MACAddressOverride" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.PSTNSoftSwitchOver" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.PSTNSoftSwitchOver" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.Host" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.Host" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_ReversePower.Status" elementDefinition="InternetGatewayDevice.X_ALU-COM_ReversePower.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_ReversePower.Status" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.TotalReminderTimes" elementDefinition="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.TotalReminderTimes" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.TotalReminderTimes" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EtsiPse.EventCode" elementDefinition="InternetGatewayDevice.X_ALU-COM_EtsiPse.EventCode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EtsiPse.EventCode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.SecondaryServerPort" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.SecondaryServerPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.SecondaryServerPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6IPAddressOrigin" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6IPAddressOrigin" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6IPAddressOrigin" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ModemPassThrough" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ModemPassThrough" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.SSID5Interface" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.SSID5Interface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.SSID5Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SpeedTest.Download" elementDefinition="InternetGatewayDevice.X_ALU-COM_SpeedTest.Download" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SpeedTest.Download" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.TrackIfName" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.TrackIfName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.TrackIfName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.ClipMode" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.ClipMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.ClipMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Enable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.RTPRedundancy" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.RTPRedundancy" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.SIP.URI" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.SIP.URI" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.ServerPort" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.ServerPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.ServerPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LANIPv6Address.{i}.Status" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LANIPv6Address.{i}.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LANIPv6Address.{i}.Status" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SRTP" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SRTP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.ToneDescriptionsEditable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.ToneDescriptionsEditable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ASB_COM_DmzIpHostCfg.InternalClient" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ASB_COM_DmzIpHostCfg.InternalClient" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ASB_COM_DmzIpHostCfg.InternalClient" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.CWMPRetryMinimumWaitInterval" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.CWMPRetryMinimumWaitInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.CWMPRetryMinimumWaitInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_PortReport2OLT.PPTP" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_PortReport2OLT.PPTP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_PortReport2OLT.PPTP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.MaxSessionsUsingRedundancy" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.MaxSessionsUsingRedundancy" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.List.{i}.Enable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.List.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.List.{i}.PacketizationPeriod" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.List.{i}.PacketizationPeriod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_RGCounters.DSPacketLossCounter" elementDefinition="InternetGatewayDevice.X_ALU-COM_RGCounters.DSPacketLossCounter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_RGCounters.DSPacketLossCounter" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.EventState" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.EventState" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.EventState" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.ACSPassword" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.ACSPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.ACSPassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Analytics.Home.SubscriptionPlan" elementDefinition="InternetGatewayDevice.X_ALU-COM_Analytics.Home.SubscriptionPlan" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Analytics.Home.SubscriptionPlan" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Ringer.DescriptionNumberOfEntries" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Ringer.DescriptionNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AppCfg.X_LinkCfg.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_AppCfg.X_LinkCfg.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AppCfg.X_LinkCfg.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU_PacketsErrored" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU_PacketsErrored" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU_PacketsErrored" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.UAMport" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.UAMport" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.UAMport" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPMode" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.UseAllocatedWAN" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.UseAllocatedWAN" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.NetMonitorDiagnostics.StartTime2" elementDefinition="InternetGatewayDevice.NetMonitorDiagnostics.StartTime2" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.NetMonitorDiagnostics.StartTime2" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.NetMonitorDiagnostics.StartTime1" elementDefinition="InternetGatewayDevice.NetMonitorDiagnostics.StartTime1" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.NetMonitorDiagnostics.StartTime1" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.PhysicalMedium.{i}.ConnectionType" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.PhysicalMedium.{i}.ConnectionType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.RegisterMode" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.RegisterMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.EventSubscribe.{i}.Event" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.EventSubscribe.{i}.Event" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ManageableDeviceNotificationLimit" elementDefinition="InternetGatewayDevice.ManagementServer.ManageableDeviceNotificationLimit" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.AutoUpdateServer" elementDefinition="InternetGatewayDevice.UserInterface.AutoUpdateServer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.VoicePortTests" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.VoicePortTests" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.PhysicalMedium.{i}.Capacity" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.PhysicalMedium.{i}.Capacity" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNEnable" elementDefinition="InternetGatewayDevice.ManagementServer.STUNEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.NetworkInUse" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.NetworkInUse" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.NetworkInUse" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_ALU-COM_802-1pMark" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_ALU-COM_802-1pMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_ALU-COM_802-1pMark" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU_OntOpticalParam.BiasCurrent" elementDefinition="InternetGatewayDevice.X_ALU_OntOpticalParam.BiasCurrent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU_OntOpticalParam.BiasCurrent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPv6DownloadDiagnosticsSupported" elementDefinition="InternetGatewayDevice.IPv6DownloadDiagnosticsSupported" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.IPv6DownloadDiagnosticsSupported" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.InterDigitTimerStd" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.InterDigitTimerStd" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.BackgroundColor" elementDefinition="InternetGatewayDevice.UserInterface.BackgroundColor" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Reset" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Reset" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.PeriodOfFullLoading" elementDefinition="InternetGatewayDevice.UploadDiagnostics.PeriodOfFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.PeriodOfFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_Authentication.WebAccount.Alias" elementDefinition="InternetGatewayDevice.X_Authentication.WebAccount.Alias" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.WebAccount.Alias" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SupportedDataTransmitRates" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SupportedDataTransmitRates" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SupportedDataTransmitRates" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.BasicDataTransferRates" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.BasicDataTransferRates" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.BasicDataTransferRates" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.SIP.EventSubscribe.{i}.AuthUserName" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.SIP.EventSubscribe.{i}.AuthUserName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.DSCPMark" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.DSCPMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ModelNumber" elementDefinition="InternetGatewayDevice.DeviceInfo.ModelNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.L2TPStartRtxDelay" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.L2TPStartRtxDelay" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.L2TPStartRtxDelay" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.ManufacturerInfo.Manufature" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.ManufacturerInfo.Manufature" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.ManufacturerInfo.Manufature" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.X_ALU_COM_FilterAPPName" elementDefinition="InternetGatewayDevice.ManagementServer.X_ALU_COM_FilterAPPName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.X_ALU_COM_FilterAPPName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ALU-COM_AllowedMACMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ALU-COM_AllowedMACMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.X_ALU-COM_AllowedMACMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.VendorLogFileNumberOfEntries" elementDefinition="InternetGatewayDevice.DeviceInfo.VendorLogFileNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FtpEnable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FtpEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FtpEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.PONLOSRecoverWait" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.PONLOSRecoverWait" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.PONLOSRecoverWait" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.Server" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.Server" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.Server" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.WanName" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.WanName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.WanName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnReqAllowedJabberIDs" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnReqAllowedJabberIDs" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnReqAllowedJabberIDs" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsErrored" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsErrored" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsErrored" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPStaticAddressNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPStaticAddressNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAAuthenticationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPAAuthenticationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.PrefixMaxNumberOfDigits" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.PrefixMaxNumberOfDigits" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.DeviceOperationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.DeviceOperationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.SupportedConnReqMethods" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.SupportedConnReqMethods" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.SupportedConnReqMethods" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.EthernetLinkStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.EthernetLinkStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnectionRequestURL" elementDefinition="InternetGatewayDevice.ManagementServer.ConnectionRequestURL" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.ChannelsInUse" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.ChannelsInUse" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.H323.FastStart" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.H323.FastStart" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_PortReport2OLT.VEIP" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_PortReport2OLT.VEIP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_PortReport2OLT.VEIP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.TotalPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.TotalPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.TotalPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.CurrentLocalTime" elementDefinition="InternetGatewayDevice.Time.CurrentLocalTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.NumberOfActiveConnections" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.NumberOfActiveConnections" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.SentDHCPOption.{i}.Alias" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.SentDHCPOption.{i}.Alias" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TestSelector" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TestSelector" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TestSelector" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LoopbackDetection.LoopCancelPeriod" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LoopbackDetection.LoopCancelPeriod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LoopbackDetection.LoopCancelPeriod" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.PacketsReceived" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.PacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetUnicastPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetUnicastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.HttpsDisabled" elementDefinition="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.HttpsDisabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.HttpsDisabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.BeaconPeriod" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.BeaconPeriod" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.BeaconPeriod" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.FaxPassThrough" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.FaxPassThrough" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.AddressingType" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.AddressingType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_WarmLineProvision" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_WarmLineProvision" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_WarmLineProvision" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Stats.BytesSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Stats.BytesSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Stats.BytesSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BeaconAdvertisementEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BeaconAdvertisementEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.DownstreamMaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.DownstreamMaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.DownstreamMaxBitRate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.CurrentAccessTechnology" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.CurrentAccessTechnology" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.CurrentAccessTechnology" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ALU-COM_CriticalDigitTimer" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ALU-COM_CriticalDigitTimer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ALU-COM_CriticalDigitTimer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.SshDisabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.SshDisabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.SshDisabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.HostList" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.HostList" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.HostList" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.PeriodicInformEnable" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.PeriodicInformEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.PeriodicInformEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AppCfg.X_EquipmentIdentity.X_CMEI.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_AppCfg.X_EquipmentIdentity.X_CMEI.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AppCfg.X_EquipmentIdentity.X_CMEI.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_DownStreamJabbers" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_DownStreamJabbers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_DownStreamJabbers" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsSentUnicast" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsSentUnicast" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsSentUnicast" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.BytesSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UPnP.Description.ServiceInstanceNumberOfEntries" elementDefinition="InternetGatewayDevice.UPnP.Description.ServiceInstanceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_BeaconInfo.OnboardingTimeout" elementDefinition="InternetGatewayDevice.X_ALU-COM_BeaconInfo.OnboardingTimeout" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_BeaconInfo.OnboardingTimeout" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_Authentication.Account.UserProfile" elementDefinition="InternetGatewayDevice.X_Authentication.Account.UserProfile" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.Account.UserProfile" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.BulkData.Profile.{i}.ReportingInterval" elementDefinition="InternetGatewayDevice.BulkData.Profile.{i}.ReportingInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.DialMode" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.DialMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.DialMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.Interface" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.Interface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_Authentication.WebAccount.Enable" elementDefinition="InternetGatewayDevice.X_Authentication.WebAccount.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.WebAccount.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Ikelifetime" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Ikelifetime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Ikelifetime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LoopbackDetection.VlanTag" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LoopbackDetection.VlanTag" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LoopbackDetection.VlanTag" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Time.NTPServer5" elementDefinition="InternetGatewayDevice.Time.NTPServer5" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NWCC.L2Server.Password" elementDefinition="InternetGatewayDevice.X_ALU-COM_NWCC.L2Server.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NWCC.L2Server.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.ManufacturerOUI" elementDefinition="InternetGatewayDevice.DeviceInfo.ManufacturerOUI" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.IPAddressUsed" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.IPAddressUsed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.IPAddressUsed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.ROMTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.ROMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.NTPServer1" elementDefinition="InternetGatewayDevice.Time.NTPServer1" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.NTPServer2" elementDefinition="InternetGatewayDevice.Time.NTPServer2" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.NTPServer3" elementDefinition="InternetGatewayDevice.Time.NTPServer3" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Time.NTPServer4" elementDefinition="InternetGatewayDevice.Time.NTPServer4" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Power" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Power" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Power" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EtsiPse.Voltage" elementDefinition="InternetGatewayDevice.X_ALU-COM_EtsiPse.Voltage" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EtsiPse.Voltage" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NWCC.L2Server.UserName" elementDefinition="InternetGatewayDevice.X_ALU-COM_NWCC.L2Server.UserName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NWCC.L2Server.UserName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACFromUserClassIDFilterExclude" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACFromUserClassIDFilterExclude" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iAuthenticationMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IEEE11iAuthenticationMode" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.X_ALU-COM_CarrierLocking.X_ALU-COM_LockingEnable" elementDefinition="InternetGatewayDevice.UserInterface.X_ALU-COM_CarrierLocking.X_ALU-COM_LockingEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UserInterface.X_ALU-COM_CarrierLocking.X_ALU-COM_LockingEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.AverageResponseTime" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.AverageResponseTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.AverageResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_NetworkProperties.UdpSessionTimer" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_NetworkProperties.UdpSessionTimer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_NetworkProperties.UdpSessionTimer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.VirtualDeviceNumberOfEntries" elementDefinition="InternetGatewayDevice.ManagementServer.VirtualDeviceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.MaxRetranCount" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.MaxRetranCount" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.UserAgentPort" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.UserAgentPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.NATDetected" elementDefinition="InternetGatewayDevice.ManagementServer.NATDetected" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.RFPower" elementDefinition="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.RFPower" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.RFPower" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ALU-COM_RingSchedule.TotalNumber" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ALU-COM_RingSchedule.TotalNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ALU-COM_RingSchedule.TotalNumber" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.Stats.BytesSent" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.Stats.BytesSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.Stats.BytesSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SpeedTest.Jitter" elementDefinition="InternetGatewayDevice.X_ALU-COM_SpeedTest.Jitter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SpeedTest.Jitter" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MESH_WDSHideSSID.SSID2G" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MESH_WDSHideSSID.SSID2G" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_MESH_WDSHideSSID.SSID2G" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.HTTPCapable" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.HTTPCapable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.HTTPCapable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.RTCP" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.RTCP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_ReversePower.IntervalStable" elementDefinition="InternetGatewayDevice.X_ALU-COM_ReversePower.IntervalStable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_ReversePower.IntervalStable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.DpdTimeout" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.DpdTimeout" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.DpdTimeout" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.PerConnectionResultNumberOfEntries" elementDefinition="InternetGatewayDevice.UploadDiagnostics.PerConnectionResultNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.PerConnectionResultNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.DownloadProgressURL" elementDefinition="InternetGatewayDevice.ManagementServer.DownloadProgressURL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_3WayCallProvision" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_3WayCallProvision" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_3WayCallProvision" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.TransmitCodec" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.TransmitCodec" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_HomeIntelligenceServer.Profile.{i}.URL" elementDefinition="InternetGatewayDevice.X_ALU-COM_HomeIntelligenceServer.Profile.{i}.URL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_HomeIntelligenceServer.Profile.{i}.URL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NonVoiceBandwidthReservedDownstream" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NonVoiceBandwidthReservedDownstream" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACAddressFilterExclude" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACAddressFilterExclude" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_ReversePower.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_ReversePower.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_ReversePower.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestMeasurementOffset" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestMeasurementOffset" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestMeasurementOffset" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UPSAlarm.Powering" elementDefinition="InternetGatewayDevice.X_ALU-COM_UPSAlarm.Powering" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UPSAlarm.Powering" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.AverageRoundTripDelay" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.AverageRoundTripDelay" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.Interface" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.Interface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.Interface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.DataModulationSupported" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.DataModulationSupported" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.PacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6ConnStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6ConnStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6ConnStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.SSID" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.SSID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.SSID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSIDAdvertisementEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSIDAdvertisementEnabled" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTLastRestoredConfig" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTLastRestoredConfig" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTLastRestoredConfig" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU_PacketsDropped" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU_PacketsDropped" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU_PacketsDropped" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.RegulatoryDomain" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.RegulatoryDomain" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_SourceIPAddress" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_SourceIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_SourceIPAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SpeedTest.ConfigTR143.{i}.UploadURL" elementDefinition="InternetGatewayDevice.X_ALU-COM_SpeedTest.ConfigTR143.{i}.UploadURL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SpeedTest.ConfigTR143.{i}.UploadURL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.TemperatureStatus.TemperatureSensor.{i}.Value" elementDefinition="InternetGatewayDevice.DeviceInfo.TemperatureStatus.TemperatureSensor.{i}.Value" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAP5" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAP5" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAP5" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.TotalBytesReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.TotalBytesReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.TotalBytesReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Stats.BytesReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Stats.BytesReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Stats.BytesReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_CallHistory" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_CallHistory" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_CallHistory" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetDiscardPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetDiscardPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.PPPDTimeout" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.PPPDTimeout" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.PPPDTimeout" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnReqJabberID" elementDefinition="InternetGatewayDevice.ManagementServer.ConnReqJabberID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_DHCPKeepAliveInterval" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_DHCPKeepAliveInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_DHCPKeepAliveInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.MaMegId" elementDefinition="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.MaMegId" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.MaMegId" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.CWMPRetryIntervalMultiplier" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.CWMPRetryIntervalMultiplier" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.CWMPRetryIntervalMultiplier" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.EnableIndividualPacketResults" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.EnableIndividualPacketResults" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.EnableIndividualPacketResults" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallForwardUnconditionalEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallForwardUnconditionalEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.LteFirmwareVer" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.LteFirmwareVer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.LteFirmwareVer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZigbeeCtrl.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZigbeeCtrl.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZigbeeCtrl.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSIDIsolate" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSIDIsolate" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSIDIsolate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.GRE.TunnelNumberOfEntries" elementDefinition="InternetGatewayDevice.GRE.TunnelNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.GRE.TunnelNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AccessPoint.Username" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AccessPoint.Username" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AccessPoint.Username" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UPnP.Discovery.RootDeviceNumberOfEntries" elementDefinition="InternetGatewayDevice.UPnP.Discovery.RootDeviceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.UploadDiagnosticsMaxIncrementalResult" elementDefinition="InternetGatewayDevice.UploadDiagnostics.UploadDiagnosticsMaxIncrementalResult" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.UploadDiagnosticsMaxIncrementalResult" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingEnable" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.MarkingEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.OutboundProxy" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.OutboundProxy" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ServerSelectionDiagnostics.ProtocolVersion" elementDefinition="InternetGatewayDevice.ServerSelectionDiagnostics.ProtocolVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ServerSelectionDiagnostics.ProtocolVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MaxLenPrompt" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MaxLenPrompt" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MaxLenPrompt" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.Manufacturer" elementDefinition="InternetGatewayDevice.DeviceInfo.Manufacturer" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.PSTNFailOver" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.PSTNFailOver" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.DevicePassword" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.DevicePassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.SupportedNbrPerLineAlarmEntries" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.SupportedNbrPerLineAlarmEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.SupportedNbrPerLineAlarmEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.IncomingCallsFailed" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.IncomingCallsFailed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.radiusPassword" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.radiusPassword" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.radiusPassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.SecondarySecret" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.SecondarySecret" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Accounting.SecondarySecret" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnectionRequestURL" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnectionRequestURL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnectionRequestURL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsSentUnicast" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsSentUnicast" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsSentUnicast" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_LogServerCfg.LogLocation" elementDefinition="InternetGatewayDevice.X_ALU-COM_LogServerCfg.LogLocation" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_LogServerCfg.LogLocation" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.ErrorsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.ErrorsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.ErrorsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6PrefixDelegationEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6PrefixDelegationEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6PrefixDelegationEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.FileBasedToneGeneration" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.FileBasedToneGeneration" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_BulkData.Status" elementDefinition="InternetGatewayDevice.X_ALU-COM_BulkData.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_BulkData.Status" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.FirstUseDate" elementDefinition="InternetGatewayDevice.DeviceInfo.FirstUseDate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.FarEndUDPPort" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.FarEndUDPPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.ProvisioningCode" elementDefinition="InternetGatewayDevice.DeviceInfo.ProvisioningCode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.SameCharPrompt" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.SameCharPrompt" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.SameCharPrompt" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.CalledNumber" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.CalledNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.CalledNumber" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MACAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MACAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Name" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.FaxT38.HighSpeedPacketRate" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.FaxT38.HighSpeedPacketRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.PhoneConnectivity" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.PhoneConnectivity" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ServiceProviderInfo.EmailAddress" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ServiceProviderInfo.EmailAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.DuplexMode" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.DuplexMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_DirectConnectUri" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_DirectConnectUri" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_DirectConnectUri" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigurationState" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.ConfigurationState" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ConnectionType" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.ConnectionType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.VLANIDMark" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.VLANIDMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Firewall.Version" elementDefinition="InternetGatewayDevice.Firewall.Version" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_FirewallLevel.Level" elementDefinition="InternetGatewayDevice.X_ALU-COM_FirewallLevel.Level" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_FirewallLevel.Level" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Capacity" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Capacity" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.Port" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.Port" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.Port" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.PrefixInformation.{i}.Prefix" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.PrefixInformation.{i}.Prefix" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.PrefixInformation.{i}.Prefix" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.BytesReceived" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.BytesReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.ResponseTime" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.ResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.RetranIntervalTimer" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.RetranIntervalTimer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_OverSizePacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_OverSizePacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_OverSizePacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.PrefixInformation.{i}.DelegatedWanConnection" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.PrefixInformation.{i}.DelegatedWanConnection" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_IPv6Config.PrefixInformation.{i}.DelegatedWanConnection" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_DestinationIPAddress" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_DestinationIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_DestinationIPAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.CTMgtIPAddress" elementDefinition="InternetGatewayDevice.ManagementServer.CTMgtIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.CTMgtIPAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.WanHttpsPort" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.WanHttpsPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.WanHttpsPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.UpstreamMaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.UpstreamMaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.UpstreamMaxBitRate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MinAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.MinAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.DoNotDisturbEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.DoNotDisturbEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.Description" elementDefinition="InternetGatewayDevice.DeviceInfo.Description" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.ReceivePacketLossRate" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.ReceivePacketLossRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.ISPHelpDesk" elementDefinition="InternetGatewayDevice.UserInterface.ISPHelpDesk" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_Op50Enabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_Op50Enabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_Op50Enabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_RGCounters.USThroughputCounter" elementDefinition="InternetGatewayDevice.X_ALU-COM_RGCounters.USThroughputCounter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_RGCounters.USThroughputCounter" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ServiceProviderInfo.Name" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ServiceProviderInfo.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPv6ServerSelectionDiagnosticsSupported" elementDefinition="InternetGatewayDevice.IPv6ServerSelectionDiagnosticsSupported" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.IPv6ServerSelectionDiagnosticsSupported" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.PrefixRange" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.PrefixRange" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.NumberOfDigitsToRemove" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.NumberOfDigitsToRemove" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.SIPEventSubscribeNumberOfElements" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.SIPEventSubscribeNumberOfElements" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.MaxValue" elementDefinition="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.MaxValue" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.MaxValue" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU_OntOpticalParam.UpperTransmitPowerThreshold" elementDefinition="InternetGatewayDevice.X_ALU_OntOpticalParam.UpperTransmitPowerThreshold" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU_OntOpticalParam.UpperTransmitPowerThreshold" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TestMode" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TestMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TestMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Status" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.NSLookupDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.NSLookupDiagnostics.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Folder.{i}.Enable" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Folder.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.NetMonitorDiagnostics.TestRequesTimes" elementDefinition="InternetGatewayDevice.NetMonitorDiagnostics.TestRequesTimes" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.NetMonitorDiagnostics.TestRequesTimes" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPSSIDInterface" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPSSIDInterface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPSSIDInterface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_CallHistoryRefresh" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_CallHistoryRefresh" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_CallHistoryRefresh" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UserInterface.ISPLogo" elementDefinition="InternetGatewayDevice.UserInterface.ISPLogo" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LoopbackDetection.LoopbackEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LoopbackDetection.LoopbackEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LoopbackDetection.LoopbackEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.HttpsDisabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.HttpsDisabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.HttpsDisabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.RingDescriptionsEditable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.RingDescriptionsEditable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.BulkData.Profile.{i}.Enable" elementDefinition="InternetGatewayDevice.BulkData.Profile.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6Prefix" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6Prefix" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6Prefix" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_BulkData.EncodingTypes" elementDefinition="InternetGatewayDevice.X_ALU-COM_BulkData.EncodingTypes" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_BulkData.EncodingTypes" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.NetMonitorDiagnostics.DataBlockSize" elementDefinition="InternetGatewayDevice.NetMonitorDiagnostics.DataBlockSize" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.NetMonitorDiagnostics.DataBlockSize" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Name" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Name" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_ReversePower.Icut" elementDefinition="InternetGatewayDevice.X_ALU-COM_ReversePower.Icut" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_ReversePower.Icut" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.EOMTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.EOMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.SoftwareModules.ExecEnvNumberOfEntries" elementDefinition="InternetGatewayDevice.SoftwareModules.ExecEnvNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.MaxClassificationEntries" elementDefinition="InternetGatewayDevice.QueueManagement.MaxClassificationEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AppCfg.X_EquipmentIdentity.X_CMEI.ConnectedURL" elementDefinition="InternetGatewayDevice.X_ALU-COM_AppCfg.X_EquipmentIdentity.X_CMEI.ConnectedURL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AppCfg.X_EquipmentIdentity.X_CMEI.ConnectedURL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.linkEventsEnabled" elementDefinition="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.linkEventsEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.linkEventsEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.WanFwMark" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.WanFwMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.WanFwMark" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBroadcastPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBroadcastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerA" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerA" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.PosOfDigitsToRemove" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.PosOfDigitsToRemove" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.L2TPRtxDelay" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.L2TPRtxDelay" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.L2TPRtxDelay" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerB" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerB" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerC" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerC" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.MPTCPEnable" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.MPTCPEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.MPTCPEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerD" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerD" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerE" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerE" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.UsbPrinterUserName" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.UsbPrinterUserName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.UsbPrinterUserName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerF" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerF" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerG" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerG" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NonVoiceBandwidthReservedUpstream" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NonVoiceBandwidthReservedUpstream" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.ZigbeeIntfStatus" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.ZigbeeIntfStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.ZigbeeIntfStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerH" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerH" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerI" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerI" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerJ" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerJ" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerK" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerK" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.SentDHCPOption.{i}.Tag" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.SentDHCPOption.{i}.Tag" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerL" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.MaxMarkingEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.MaxMarkingEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerM" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerM" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.TimerM" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6DNSServers" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6DNSServers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6DNSServers" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_ALU-COM_RadioRetranscount" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_ALU-COM_RadioRetranscount" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.X_ALU-COM_RadioRetranscount" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.IcmpEchoReqDisabled" elementDefinition="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.IcmpEchoReqDisabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.IcmpEchoReqDisabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.EnablePerConnectionResults" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.EnablePerConnectionResults" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.EnablePerConnectionResults" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Alias" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Alias" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DNSServers" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DNSServers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.X_ALU-COM_MaxPolicyEntries" elementDefinition="InternetGatewayDevice.QueueManagement.X_ALU-COM_MaxPolicyEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.QueueManagement.X_ALU-COM_MaxPolicyEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.LCPEchoFailure" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.LCPEchoFailure" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.LCPEchoFailure" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AccessPoint.Password" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AccessPoint.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AccessPoint.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.TotalPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.TotalPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.TotalPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.NSLookupDiagnostics.Interface" elementDefinition="InternetGatewayDevice.NSLookupDiagnostics.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.NSLookupDiagnostics.SuccessCount" elementDefinition="InternetGatewayDevice.NSLookupDiagnostics.SuccessCount" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ServiceProviderInfo.ContactPhoneNumber" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ServiceProviderInfo.ContactPhoneNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.TelnetDisabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.TelnetDisabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.TelnetDisabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Stats.PacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Stats.PacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Stats.PacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.SessionDuration" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.SessionDuration" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Password" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestMeasurementOffset" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestMeasurementOffset" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TimeBasedTestMeasurementOffset" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_WifiSchedule.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_WifiSchedule.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_WifiSchedule.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SessionStartTime" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SessionStartTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SessionStartTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AppCfg.DnsProxyCfg.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_AppCfg.DnsProxyCfg.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AppCfg.DnsProxyCfg.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_ReversePower.IntervalSlack" elementDefinition="InternetGatewayDevice.X_ALU-COM_ReversePower.IntervalSlack" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_ReversePower.IntervalSlack" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.PortMappingNumberOfEntries" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.PortMappingNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.PacketsReceived" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.PacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.PacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.OnBoardStatus" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.OnBoardStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.OnBoardStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_AC_Hazardous_Voltage_thld-Volt" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_AC_Hazardous_Voltage_thld-Volt" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_AC_Hazardous_Voltage_thld-Volt" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPv4DownloadDiagnosticsSupported" elementDefinition="InternetGatewayDevice.IPv4DownloadDiagnosticsSupported" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.IPv4DownloadDiagnosticsSupported" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IoTAppUser.IoTAppAccount.{i}.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IoTAppUser.IoTAppAccount.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IoTAppUser.IoTAppAccount.{i}.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotFirmwareInfo.{i}.IOTDownloadFailReason" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotFirmwareInfo.{i}.IOTDownloadFailReason" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotFirmwareInfo.{i}.IOTDownloadFailReason" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.NetworkServer.NFSEnable" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.NetworkServer.NFSEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.OperatorUniqueID" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.OperatorUniqueID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.OperatorUniqueID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.UUID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.UUID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Resistance_Tip_Ground-Kohm" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Resistance_Tip_Ground-Kohm" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Resistance_Tip_Ground-Kohm" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACFromClientIDFilter" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACFromClientIDFilter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SpeedTest.DiagnosticsState" elementDefinition="InternetGatewayDevice.X_ALU-COM_SpeedTest.DiagnosticsState" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SpeedTest.DiagnosticsState" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.LteChannelQuality" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.LteChannelQuality" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.LteChannelQuality" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Location_Capable" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Location_Capable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Location_Capable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_ALU-COM_WANUSBDongleLinkConfig.MACAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_ALU-COM_WANUSBDongleLinkConfig.MACAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_ALU-COM_WANUSBDongleLinkConfig.MACAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UserInterface.WarrantyDate" elementDefinition="InternetGatewayDevice.UserInterface.WarrantyDate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceived" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.InUseProfileReference" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.InUseProfileReference" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.InUseProfileReference" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SessionDirection" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SessionDirection" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.SessionDirection" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPServerSecret" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPServerSecret" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPServerSecret" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AppCfg.OperatorPlugins.ProvinceCode" elementDefinition="InternetGatewayDevice.X_ALU-COM_AppCfg.OperatorPlugins.ProvinceCode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AppCfg.OperatorPlugins.ProvinceCode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsSentBroadcast" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsSentBroadcast" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.X_ALU_PacketsSentBroadcast" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PossibleChannels" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PossibleChannels" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.EthernetTaggingCoupled" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.EthernetTaggingCoupled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.Stats.PacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ServiceProviderInfo.URL" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ServiceProviderInfo.URL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SpeedTest.Location" elementDefinition="InternetGatewayDevice.X_ALU-COM_SpeedTest.Location" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SpeedTest.Location" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZwaveCtrl.Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZwaveCtrl.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZwaveCtrl.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.RadioReference" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.RadioReference" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.RadioReference" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SambaEnable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SambaEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SambaEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_BeaconInfo.AutoBackhaulLinkSwitching" elementDefinition="InternetGatewayDevice.X_ALU-COM_BeaconInfo.AutoBackhaulLinkSwitching" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_BeaconInfo.AutoBackhaulLinkSwitching" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.URL" elementDefinition="InternetGatewayDevice.ManagementServer.URL" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.SuccessCount" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.SuccessCount" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.SuccessCount" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.TLSAuthenticationProtocols" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.TLSAuthenticationProtocols" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.DSCPMark" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.DSCPMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.AutoChannelEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NWCC.L1Server.ClientID" elementDefinition="InternetGatewayDevice.X_ALU-COM_NWCC.L1Server.ClientID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NWCC.L1Server.ClientID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.SIP.EventSubscribe.{i}.Event" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.SIP.EventSubscribe.{i}.Event" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.UploadURL" elementDefinition="InternetGatewayDevice.UploadDiagnostics.UploadURL" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Ringer_Equiv_Max_Thld-mREN" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Ringer_Equiv_Max_Thld-mREN" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Ringer_Equiv_Max_Thld-mREN" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.MaxSessionCount" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.MaxSessionCount" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TestFileLength" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TestFileLength" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.Tr69Disabled" elementDefinition="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.Tr69Disabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_LanAccessCfg.Tr69Disabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.RingPatternEditable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.RingPatternEditable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.X_ALU-COM_Option60Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.X_ALU-COM_Option60Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.X_ALU-COM_Option60Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKey.{i}.WEPKey" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WEPKey.{i}.WEPKey" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MACAddressControlEnabled" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MACAddressControlEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.HTTPSCapable" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.HTTPSCapable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.HTTPSCapable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.CallsDropped" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.CallsDropped" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.ExampleLogin" elementDefinition="InternetGatewayDevice.UserInterface.ExampleLogin" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.FacilityAction" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfo.{i}.FacilityAction" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.BroadcastPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.BroadcastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.BroadcastPacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.IPAddressUsed" elementDefinition="InternetGatewayDevice.UploadDiagnostics.IPAddressUsed" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.IPAddressUsed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnectionRequestUsername" elementDefinition="InternetGatewayDevice.ManagementServer.ConnectionRequestUsername" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Status" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.IPPingDiagnostics.AverageResponseTime" elementDefinition="InternetGatewayDevice.IPPingDiagnostics.AverageResponseTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SftpEnable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SftpEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SftpEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.Gatekeeper" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.Gatekeeper" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IoTAppUser.IoTAppAccount.{i}.Username" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IoTAppUser.IoTAppAccount.{i}.Username" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IoTAppUser.IoTAppAccount.{i}.Username" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_RGCounters.DNSResponseTime" elementDefinition="InternetGatewayDevice.X_ALU-COM_RGCounters.DNSResponseTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_RGCounters.DNSResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceived" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.FilterNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.FilterNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.SSIDInterface" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.SSIDInterface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.SSIDInterface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_DownStreamBwUtilization" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_DownStreamBwUtilization" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_DownStreamBwUtilization" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FactoryTelnetEnable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FactoryTelnetEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.FactoryTelnetEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TG_RG_Foreign_ACV_thld-Volt" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TG_RG_Foreign_ACV_thld-Volt" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TG_RG_Foreign_ACV_thld-Volt" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_ALU-COM_Mode" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_ALU-COM_Mode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANEthernetLinkConfig.X_ALU-COM_Mode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BeaconType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.BeaconType" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.DiagnosticsState" elementDefinition="InternetGatewayDevice.UploadDiagnostics.DiagnosticsState" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.PhysicalMedium.{i}.Status" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.PhysicalMedium.{i}.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_CT-COM_WANGponLinkConfig.802-1pMark" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_CT-COM_WANGponLinkConfig.802-1pMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_CT-COM_WANGponLinkConfig.802-1pMark" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BytesSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU_COM_ChannelBandWidthExtend" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU_COM_ChannelBandWidthExtend" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU_COM_ChannelBandWidthExtend" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.NetworkServer.AFPEnable" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.NetworkServer.AFPEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_UnderSizePacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_UnderSizePacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_UnderSizePacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACFromVendorClassIDFilterExclude" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACFromVendorClassIDFilterExclude" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.PhysicalMedium.{i}.Removable" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.PhysicalMedium.{i}.Removable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.CtLanPortsBindCfg.BindedLanList" elementDefinition="InternetGatewayDevice.CtLanPortsBindCfg.BindedLanList" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.CtLanPortsBindCfg.BindedLanList" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.EthernetPriorityMark" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.EthernetPriorityMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SpeedTest.Latency" elementDefinition="InternetGatewayDevice.X_ALU-COM_SpeedTest.Latency" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SpeedTest.Latency" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_WOLAN.PublicPort" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_WOLAN.PublicPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_WOLAN.PublicPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_DefaultIPv6Gateway" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_DefaultIPv6Gateway" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_DefaultIPv6Gateway" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.MaximumResponseTime" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.MaximumResponseTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.MaximumResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.ActiveUplink" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.ActiveUplink" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.ActiveUplink" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ButtonMap.Button.{i}.QuickDialNumber" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ButtonMap.Button.{i}.QuickDialNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EtsiPse.SRiClassCfg" elementDefinition="InternetGatewayDevice.X_ALU-COM_EtsiPse.SRiClassCfg" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EtsiPse.SRiClassCfg" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SignalingProtocols" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SignalingProtocols" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceivedUnderFullLoading" elementDefinition="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceivedUnderFullLoading" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.TotalBytesReceivedUnderFullLoading" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IsolationEnable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IsolationEnable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.IsolationEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnectionRequestUsername" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnectionRequestUsername" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.ConnectionRequestUsername" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.AdmitOnlyVLANTagged" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.AdmitOnlyVLANTagged" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.SIP.AuthPassword" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.SIP.AuthPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.TransmitPacketizationPeriod" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.TransmitPacketizationPeriod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.UserUpdateServer" elementDefinition="InternetGatewayDevice.UserInterface.UserUpdateServer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.EventSubscription" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.EventSubscription" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SshPort" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SshPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SshPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Folder.{i}.UserAccountAccess" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Folder.{i}.UserAccountAccess" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.FlashHookMax" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.FlashHookMax" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.FlashHookMax" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.PIN" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.PIN" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.PIN" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UserInterface.PasswordUserSelectable" elementDefinition="InternetGatewayDevice.UserInterface.PasswordUserSelectable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.OamId" elementDefinition="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.OamId" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.OamId" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.TLSKeyExchangeProtocols" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.TLSKeyExchangeProtocols" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_BulkData.ParameterWildCardSupported" elementDefinition="InternetGatewayDevice.X_ALU-COM_BulkData.ParameterWildCardSupported" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_BulkData.ParameterWildCardSupported" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfileNumberOfEntries" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfileNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsReceivedMulticast" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsReceivedMulticast" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsReceivedMulticast" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_DownStreamJabbers" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_DownStreamJabbers" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_DownStreamJabbers" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.X_ALU_COM_CurMaxBitRate" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.X_ALU_COM_CurMaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.X_ALU_COM_CurMaxBitRate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.TransmitBitRate" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.TransmitBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.Interface" elementDefinition="InternetGatewayDevice.UDPEchoConfig.Interface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.VoiceProcessing.EchoCancellationInUse" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.VoiceProcessing.EchoCancellationInUse" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.MaxMTUSize" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.MaxMTUSize" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_PacketsLost" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_PacketsLost" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_PacketsLost" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.InformParameterNumberOfEntries" elementDefinition="InternetGatewayDevice.ManagementServer.InformParameterNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANEthernetInterfaceConfig.MaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.Status" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.Status" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.TotalPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UPnP.Device.Capabilities.UPnPArchitecture" elementDefinition="InternetGatewayDevice.UPnP.Device.Capabilities.UPnPArchitecture" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.OperatingStandards" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.OperatingStandards" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.OperatingStandards" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU_OntOpticalParam.Enable" elementDefinition="InternetGatewayDevice.X_ALU_OntOpticalParam.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU_OntOpticalParam.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.RoundTripDelay" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.RoundTripDelay" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EtsiPse.Reset" elementDefinition="InternetGatewayDevice.X_ALU-COM_EtsiPse.Reset" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EtsiPse.Reset" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.ErrorsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.ErrorsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.ErrorsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.URL" elementDefinition="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.URL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.URN" elementDefinition="InternetGatewayDevice.DeviceInfo.SupportedDataModel.{i}.URN" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.UsbPrinterEnable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.UsbPrinterEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.UsbPrinterEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.ConnReqXMPPConnection" elementDefinition="InternetGatewayDevice.ManagementServer.ConnReqXMPPConnection" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_BeaconInfo.BeaconNumberofEntries" elementDefinition="InternetGatewayDevice.X_ALU-COM_BeaconInfo.BeaconNumberofEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_BeaconInfo.BeaconNumberofEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadDiagnosticMaxConnections" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.DownloadDiagnosticMaxConnections" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.DownloadDiagnosticMaxConnections" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfoNumberOfEntries" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.PrefixInfoNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.ExclusivityOrder" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.ExclusivityOrder" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_LogServerCfg.SFTPusername" elementDefinition="InternetGatewayDevice.X_ALU-COM_LogServerCfg.SFTPusername" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_LogServerCfg.SFTPusername" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.LastChange" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.LastChange" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.LastChange" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AccessPoint.APN" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AccessPoint.APN" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AccessPoint.APN" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPServerAuthPort" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPServerAuthPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPServerAuthPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Status" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Status" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSID" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.SSID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LANIPv6Address.{i}.Origin" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LANIPv6Address.{i}.Origin" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LANIPv6Address.{i}.Origin" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.IPv6UploadDiagnosticsSupported" elementDefinition="InternetGatewayDevice.IPv6UploadDiagnosticsSupported" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.IPv6UploadDiagnosticsSupported" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.EnableCWMP" elementDefinition="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.EnableCWMP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SaaSManagementServer.EnableCWMP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Authtype" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Authtype" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Authtype" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_AppCfg.OperatorPlugins.plugin.{i}.Name" elementDefinition="InternetGatewayDevice.X_ALU-COM_AppCfg.OperatorPlugins.plugin.{i}.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_AppCfg.OperatorPlugins.plugin.{i}.Name" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.EnabledForInternet" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.EnabledForInternet" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.TunnelPort" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.TunnelPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.TunnelPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPStaticAddress.{i}.Alias" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPStaticAddress.{i}.Alias" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.NetMonitorDiagnostics.Switch" elementDefinition="InternetGatewayDevice.NetMonitorDiagnostics.Switch" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.NetMonitorDiagnostics.Switch" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.ReceiveCodec" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.ReceiveCodec" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ButtonMap.Button.{i}.UserAccess" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ButtonMap.Button.{i}.UserAccess" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.MinSE" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.MinSE" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.MinSE" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Alias" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Alias" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.IcmpEchoReqTrusted" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.IcmpEchoReqTrusted" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.IcmpEchoReqTrusted" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.H323.H323ID" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.H323.H323ID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.PacketsResponded" elementDefinition="InternetGatewayDevice.UDPEchoConfig.PacketsResponded" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SpeedTest.ConfigTR143NumberOfEntries" elementDefinition="InternetGatewayDevice.X_ALU-COM_SpeedTest.ConfigTR143NumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SpeedTest.ConfigTR143NumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_MACAddressesDescription" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_MACAddressesDescription" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_MACAddressesDescription" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.FarEndInterarrivalJitter" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.FarEndInterarrivalJitter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.CWMPRetryIntervalMultiplier" elementDefinition="InternetGatewayDevice.ManagementServer.CWMPRetryIntervalMultiplier" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnicastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.UnicastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.VolumeEncryptionCapable" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.VolumeEncryptionCapable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.StorageService.{i}.Capabilites.VolumeEncryptionCapable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TG_RG_Foreign_DCV_thld-Volt" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TG_RG_Foreign_DCV_thld-Volt" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TG_RG_Foreign_DCV_thld-Volt" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.BroadcastPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Stats.BroadcastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ALU-COM_StartDigitTimer" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ALU-COM_StartDigitTimer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ALU-COM_StartDigitTimer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACAddressFilterList" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.SourceMACAddressFilterList" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Encrypted" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.LogicalVolume.{i}.Encrypted" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.MinValue" elementDefinition="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.MinValue" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.MinValue" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Hazardous_TestResult" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Hazardous_TestResult" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Hazardous_TestResult" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.DiscardPacketsSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.DiscardPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.ServiceAffecting" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.ServiceAffecting" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.ServiceAffecting" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.ResultNumberOfEntries" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.ResultNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.ResultNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_CallWaitingProvision" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_CallWaitingProvision" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.X_ALU-COM_CallWaitingProvision" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.BulkData.Profile.{i}.HTTP.{i}.Username" elementDefinition="InternetGatewayDevice.BulkData.Profile.{i}.HTTP.{i}.Username" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.BulkData.Profile.{i}.HTTP.{i}.Username" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.X_ALU-COM_EnableServerCertValidation" elementDefinition="InternetGatewayDevice.ManagementServer.X_ALU-COM_EnableServerCertValidation" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.X_ALU-COM_EnableServerCertValidation" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.X_ALU-COM_ClassifierNumberOfEntries" elementDefinition="InternetGatewayDevice.QueueManagement.X_ALU-COM_ClassifierNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.QueueManagement.X_ALU-COM_ClassifierNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.DpdDelay" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.DpdDelay" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.DpdDelay" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AccessPoint.DialNumber" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AccessPoint.DialNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AccessPoint.DialNumber" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.TxRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.TxRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.TxRate" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.AppNumberOfEntries" elementDefinition="InternetGatewayDevice.QueueManagement.AppNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6IPAddress" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6IPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_IPv6IPAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.TLSEncryptionProtocols" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.TLSEncryptionProtocols" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.LoggedReminderTime.{i}.LastReminderTime" elementDefinition="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.LoggedReminderTime.{i}.LastReminderTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_PortalChangePassword.LoggedReminderTime.{i}.LastReminderTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_BeaconInfo.MaxNumberOfBeacons" elementDefinition="InternetGatewayDevice.X_ALU-COM_BeaconInfo.MaxNumberOfBeacons" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_BeaconInfo.MaxNumberOfBeacons" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Ringer_Equiv_Min_Thld-mREN" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Ringer_Equiv_Min_Thld-mREN" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Ringer_Equiv_Min_Thld-mREN" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.TelnetUserName" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.TelnetUserName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.TelnetUserName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.FlashHookMin" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.FlashHookMin" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.X_ASB_COM_VOICECONFIG.FlashHookMin" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestDuration" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestDuration" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.TimeBasedTestDuration" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1UpstreamMaxBitRate" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.Layer1UpstreamMaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.KickURL" elementDefinition="InternetGatewayDevice.ManagementServer.KickURL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.NetMonitorDiagnostics.EndTime1" elementDefinition="InternetGatewayDevice.NetMonitorDiagnostics.EndTime1" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.NetMonitorDiagnostics.EndTime1" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.Reset" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.Reset" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.Reset" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LANIPv6Address.{i}.IPAddress" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LANIPv6Address.{i}.IPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LANIPv6Address.{i}.IPAddress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.NetMonitorDiagnostics.EndTime2" elementDefinition="InternetGatewayDevice.NetMonitorDiagnostics.EndTime2" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.NetMonitorDiagnostics.EndTime2" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.ConferenceCallingStatus" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.ConferenceCallingStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalBytesSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalBytesSent" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_ReceiveInterarrivalJitter" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_ReceiveInterarrivalJitter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_ReceiveInterarrivalJitter" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.ToneFileFormats" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.ToneFileFormats" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Pskey" elementDefinition="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Pskey" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_VPNDevice.VPNClient.Pskey" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.BlockPayloadType" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.BlockPayloadType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU_COM_PreConfig.X_ALU_COM_WANKeyParamsDelayActive" elementDefinition="InternetGatewayDevice.X_ALU_COM_PreConfig.X_ALU_COM_WANKeyParamsDelayActive" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU_COM_PreConfig.X_ALU_COM_WANKeyParamsDelayActive" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.VoiceProcessing.EchoCancellationEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.VoiceProcessing.EchoCancellationEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU_OntOpticalParam.RXPower" elementDefinition="InternetGatewayDevice.X_ALU_OntOpticalParam.RXPower" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU_OntOpticalParam.RXPower" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_UpStreamFragments" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_UpStreamFragments" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_UpStreamFragments" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TR_Resistance_thld-Kohm" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TR_Resistance_thld-Kohm" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TR_Resistance_thld-Kohm" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AccessPoint.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AccessPoint.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AccessPoint.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsDropped" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsDropped" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsDropped" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.Interface" elementDefinition="InternetGatewayDevice.UploadDiagnostics.Interface" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.Underruns" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.Underruns" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.RegistrarServerPort" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.RegistrarServerPort" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.LinkStatus" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.LinkStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU_OntOpticalParam.SupplyVottage" elementDefinition="InternetGatewayDevice.X_ALU_OntOpticalParam.SupplyVottage" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU_OntOpticalParam.SupplyVottage" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.PatternBasedRingGeneration" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.PatternBasedRingGeneration" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Status" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Status" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.MepId" elementDefinition="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.MepId" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8021ag1731Cfg.MepId" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ExactDigitMap" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ExactDigitMap" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ExactDigitMap" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetUnicastPacketsSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetUnicastPacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ButtonMap.Button.{i}.ButtonMessage" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ButtonMap.Button.{i}.ButtonMessage" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_HomeIntelligenceServer.Profile.{i}.Password" elementDefinition="InternetGatewayDevice.X_ALU-COM_HomeIntelligenceServer.Profile.{i}.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_HomeIntelligenceServer.Profile.{i}.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallForwardOnBusyNumber" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallForwardOnBusyNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Marking.{i}.EthernetPriorityOverride" elementDefinition="InternetGatewayDevice.Layer2Bridging.Marking.{i}.EthernetPriorityOverride" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.DiscardPacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.DiscardPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_WLANInterfaceConfig.Stats.DiscardPacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACFromVendorClassIDFilter" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACFromVendorClassIDFilter" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.SetupLock" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.WPS.SetupLock" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_isFixedWAN" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_isFixedWAN" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_isFixedWAN" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.ImplicitRegistrationEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.ImplicitRegistrationEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.ImplicitRegistrationEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_BeaconInfo.LegalSN" elementDefinition="InternetGatewayDevice.X_ALU-COM_BeaconInfo.LegalSN" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_BeaconInfo.LegalSN" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_SwMgnt.X_ALU-COM_Polling_URL" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_SwMgnt.X_ALU-COM_Polling_URL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_SwMgnt.X_ALU-COM_Polling_URL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ButtonMap.Button.{i}.FacilityAction" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.ButtonMap.Button.{i}.FacilityAction" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.Stats.PacketsSent" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.Stats.PacketsSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.Stats.PacketsSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPStaticAddress.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPStaticAddress.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_ReversePower.CurrentPercent" elementDefinition="InternetGatewayDevice.X_ALU-COM_ReversePower.CurrentPercent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_ReversePower.CurrentPercent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.SSID5" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.SSID5" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.SSID5" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZigbeeCtrl.Reset" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZigbeeCtrl.Reset" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZigbeeCtrl.Reset" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBytesReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.EthernetBytesReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.NetworkSelection.AvailableNetworks" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.NetworkSelection.AvailableNetworks" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.NetworkSelection.AvailableNetworks" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MaxBitRate" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.MaxBitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.DefaultForwardingPolicy" elementDefinition="InternetGatewayDevice.QueueManagement.DefaultForwardingPolicy" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.VLANIDMark" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.VLANIDMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.Host" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.Host" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.Host" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.Organization" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.Organization" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.ISPLogoSize" elementDefinition="InternetGatewayDevice.UserInterface.ISPLogoSize" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPSKFailures" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.TotalPSKFailures" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.radiusServerIp" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.radiusServerIp" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.radiusServerIp" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_AutoChannelRefreshPeriod" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_AutoChannelRefreshPeriod" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.X_ALU-COM_AutoChannelRefreshPeriod" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UploadDiagnosticsMaxIncrementalResult" elementDefinition="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UploadDiagnosticsMaxIncrementalResult" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Capabilities.PerformanceDiagnostic.UploadDiagnosticsMaxIncrementalResult" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.EventSubscribe.{i}.NotifierTransport" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.EventSubscribe.{i}.NotifierTransport" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.VendorConfigFile.{i}.Name" elementDefinition="InternetGatewayDevice.DeviceInfo.VendorConfigFile.{i}.Name" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallTransferEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.CallTransferEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.ManufacturerInfo.Model" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.ManufacturerInfo.Model" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.ManufacturerInfo.Model" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.PhysicalMediumNumberOfEntries" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.PhysicalMediumNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SshEnable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SshEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SshEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_RouterAdvertisement.MaxRtrAdvInterval" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_RouterAdvertisement.MaxRtrAdvInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_RouterAdvertisement.MaxRtrAdvInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.L2TPMaxRetry" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.L2TPMaxRetry" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.L2TP.L2TPMaxRetry" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.WANAccessType" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANCommonInterfaceConfig.WANAccessType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_DownStreamFragments" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_DownStreamFragments" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU-COM_DownStreamFragments" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsSentMulticast" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsSentMulticast" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.Stats.X_ALU_PacketsSentMulticast" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.RegistersMinExpires" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.RegistersMinExpires" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.ErrorsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.MWIEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.MWIEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_DownStreamBwUtilization" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_DownStreamBwUtilization" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_DownStreamBwUtilization" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.GRE.X_ALU-COM_MAXNumberOfTunnelEntries" elementDefinition="InternetGatewayDevice.GRE.X_ALU-COM_MAXNumberOfTunnelEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.GRE.X_ALU-COM_MAXNumberOfTunnelEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.AvailableInterfaceNumberOfEntries" elementDefinition="InternetGatewayDevice.Layer2Bridging.AvailableInterfaceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PossibleDataTransmitRates" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PossibleDataTransmitRates" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.IPAddressUsed" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.IPAddressUsed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.IPAddressUsed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_Authentication.Account.Enable" elementDefinition="InternetGatewayDevice.X_Authentication.Account.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.Account.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LoopbackDetection.LoopExistPeriod" elementDefinition="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LoopbackDetection.LoopExistPeriod" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.X_ALU-COM_LoopbackDetection.LoopExistPeriod" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU_OntOpticalParam.TXPower" elementDefinition="InternetGatewayDevice.X_ALU_OntOpticalParam.TXPower" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU_OntOpticalParam.TXPower" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.QueueNumberOfEntries" elementDefinition="InternetGatewayDevice.QueueManagement.QueueNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UserInterface.ISPName" elementDefinition="InternetGatewayDevice.UserInterface.ISPName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_ReversePower.TryAgainCount" elementDefinition="InternetGatewayDevice.X_ALU-COM_ReversePower.TryAgainCount" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_ReversePower.TryAgainCount" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AvailableNetworks" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AvailableNetworks" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.AvailableNetworks" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.BytesReceived" elementDefinition="InternetGatewayDevice.UDPEchoConfig.BytesReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPSSID" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPSSID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.EAPSSID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Resistance_Tip_Ring-Kohm" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Resistance_Tip_Ring-Kohm" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_Resistance_Tip_Ring-Kohm" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTServerConfigURL" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTServerConfigURL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTServerConfigURL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.FlowNumberOfEntries" elementDefinition="InternetGatewayDevice.QueueManagement.FlowNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.Stats.ByteReceived" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.Stats.ByteReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.Stats.ByteReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTServerID" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTServerID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTServerID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_PwrMngtCfg.X_ALU-COM_EthAutoPwrDwnEn" elementDefinition="InternetGatewayDevice.X_ALU-COM_PwrMngtCfg.X_ALU-COM_EthAutoPwrDwnEn" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_PwrMngtCfg.X_ALU-COM_EthAutoPwrDwnEn" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AccessPoint.Password" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AccessPoint.Password" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.AccessPoint.Password" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTHWVersion" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTHWVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWInfo.IOTHWVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.NumberOfConnections" elementDefinition="InternetGatewayDevice.UploadDiagnostics.NumberOfConnections" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UploadDiagnostics.NumberOfConnections" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_SwMgnt.X_ALU-COM_Enable" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_SwMgnt.X_ALU-COM_Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.X_ALU-COM_SwMgnt.X_ALU-COM_Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.List.{i}.SilenceSuppression" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.List.{i}.SilenceSuppression" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.PacketsLost" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.PacketsLost" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.X_ALU-COM_Hist_Session.{i}.PacketsLost" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.MaxQueueEntries" elementDefinition="InternetGatewayDevice.QueueManagement.MaxQueueEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceSubnetMask" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceSubnetMask" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EtsiPse.PseOperationalClass" elementDefinition="InternetGatewayDevice.X_ALU-COM_EtsiPse.PseOperationalClass" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EtsiPse.PseOperationalClass" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.TemperatureStatus.TemperatureSensor.{i}.Status" elementDefinition="InternetGatewayDevice.DeviceInfo.TemperatureStatus.TemperatureSensor.{i}.Status" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.MaxLineCount" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.MaxLineCount" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SRTPKeyingMethods" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SRTPKeyingMethods" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.AnonymousCallEnable" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.AnonymousCallEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.CallingFeatures.AnonymousCallEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZwaveCtrl.ZWaveConfigRestoreStatus" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZwaveCtrl.ZWaveConfigRestoreStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotZwaveCtrl.ZWaveConfigRestoreStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UploadDiagnostics.BOMTime" elementDefinition="InternetGatewayDevice.UploadDiagnostics.BOMTime" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotFirmwareInfo.{i}.IOTDownloadStatus" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotFirmwareInfo.{i}.IOTDownloadStatus" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotFirmwareInfo.{i}.IOTDownloadStatus" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DNSEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DNSEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.AGCOffset" elementDefinition="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.AGCOffset" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_RFVideoDevice.AGCOffset" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DNSOverrideAllowed" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DNSOverrideAllowed" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.DSCP" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.DSCP" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.DSCP" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.NetInfo.DomainName" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.NetInfo.DomainName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_CRCErrorReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_CRCErrorReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_CRCErrorReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BroadcastPacketsReceived" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.BroadcastPacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.InvalidNumberTone" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.InvalidNumberTone" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.SteeringEnable" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.SteeringEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.SteeringEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Enable" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.Enable" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.MSISDN" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.MSISDN" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.USIM.MSISDN" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.SupportedAccessTechnologies" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.SupportedAccessTechnologies" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.SupportedAccessTechnologies" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.EthertypeFilterList" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.EthertypeFilterList" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.TrackFailSwitchDelay" elementDefinition="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.TrackFailSwitchDelay" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_UplinkManagement.X_ALU-COM_SwitchOverLogic.TrackFailSwitchDelay" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.AdminState" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.AdminState" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.X_ALU-COM_FaultMgnt.Line.{i}.SupportedAlarm.{i}.AdminState" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_HomeIntelligenceServer.Profile.{i}.TenantID" elementDefinition="InternetGatewayDevice.X_ALU-COM_HomeIntelligenceServer.Profile.{i}.TenantID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_HomeIntelligenceServer.Profile.{i}.TenantID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Stats.PacketsReceived" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Stats.PacketsReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.Stats.PacketsReceived" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.X_ALU-COM_DSCPMark" elementDefinition="InternetGatewayDevice.ManagementServer.X_ALU-COM_DSCPMark" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.X_ALU-COM_DSCPMark" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_CRCErrorSent" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_CRCErrorSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.LANEthernetInterfaceConfig.{i}.Stats.X_ALU-COM_CRCErrorSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.EmailSupport" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.EmailSupport" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.EmailSupport" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.ProcessStatus.CPUUsage" elementDefinition="InternetGatewayDevice.DeviceInfo.ProcessStatus.CPUUsage" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.InterDigitTimerOpen" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.NumberingPlan.InterDigitTimerOpen" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.QueueManagement.AvailableAppList" elementDefinition="InternetGatewayDevice.QueueManagement.AvailableAppList" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.SerialNumber" elementDefinition="InternetGatewayDevice.DeviceInfo.SerialNumber" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU_COM_BandSteering.Enable" elementDefinition="InternetGatewayDevice.X_ALU_COM_BandSteering.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU_COM_BandSteering.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.STUNServerAddress" elementDefinition="InternetGatewayDevice.ManagementServer.STUNServerAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_PwrMngtCfg.X_ALU-COM_EthEEE" elementDefinition="InternetGatewayDevice.X_ALU-COM_PwrMngtCfg.X_ALU-COM_EthEEE" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_PwrMngtCfg.X_ALU-COM_EthEEE" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SftpRemoteAccessEnable" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SftpRemoteAccessEnable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.SftpRemoteAccessEnable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Ringer.EventNumberOfEntries" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Ringer.EventNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Requested_Location_Info" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Requested_Location_Info" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Requested_Location_Info" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.PerConnectionResultNumberOfEntries" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.PerConnectionResultNumberOfEntries" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.PerConnectionResultNumberOfEntries" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SpeedTest.ServerName" elementDefinition="InternetGatewayDevice.X_ALU-COM_SpeedTest.ServerName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SpeedTest.ServerName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_D0542D_ServiceList" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_D0542D_ServiceList" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_D0542D_ServiceList" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.X_ALU-COM_XML_File_Name_Path" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.X_ALU-COM_XML_File_Name_Path" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.SIP.X_ALU-COM_XML_File_Name_Path" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceAddressingType" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.IPInterface.{i}.IPInterfaceAddressingType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.AutoDisconnectTime" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.AutoDisconnectTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NWCC.L1Server.URL" elementDefinition="InternetGatewayDevice.X_ALU-COM_NWCC.L1Server.URL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NWCC.L1Server.URL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.X_AcsPeriodicInformInterval" elementDefinition="InternetGatewayDevice.ManagementServer.X_AcsPeriodicInformInterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.ManagementServer.X_AcsPeriodicInformInterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.WANInterface" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.WANInterface" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.WANInterface" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.NATEnabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.NATEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.VendorConfigFile.{i}.Description" elementDefinition="InternetGatewayDevice.DeviceInfo.VendorConfigFile.{i}.Description" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Ookla.ServerId" elementDefinition="InternetGatewayDevice.X_ALU-COM_Ookla.ServerId" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Ookla.ServerId" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.FarEndIPAddress" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.FarEndIPAddress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.ModemRedundancy" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.ModemRedundancy" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.Tr69Disabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.Tr69Disabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.Tr69Disabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PreSharedKey.{i}.KeyPassphrase" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.PreSharedKey.{i}.KeyPassphrase" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UPnP.Description.DeviceInstanceNumberOfEntries" elementDefinition="InternetGatewayDevice.UPnP.Description.DeviceInstanceNumberOfEntries" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTAppServerURL" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTAppServerURL" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTAppServerURL" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Analytics.Home.SubscriberID" elementDefinition="InternetGatewayDevice.X_ALU-COM_Analytics.Home.SubscriberID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Analytics.Home.SubscriberID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.FtpDisabled" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.FtpDisabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.FtpDisabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_CallingNumber" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_CallingNumber" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Session.{i}.X_ALU-COM_CallingNumber" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceived" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceived" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.AliasBasedAddressing" elementDefinition="InternetGatewayDevice.ManagementServer.AliasBasedAddressing" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.X_ALU_DHCPOption125.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.X_ALU_DHCPOption125.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.X_ALU_DHCPOption125.Enable" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.LinkType" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANPOTSLinkConfig.LinkType" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.UDPEchoDiagnostics.AverageResponseTime" elementDefinition="InternetGatewayDevice.UDPEchoDiagnostics.AverageResponseTime" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.UDPEchoDiagnostics.AverageResponseTime" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.AssociatedConnection" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.AssociatedConnection" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.radiusPort" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.radiusPort" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.radiusPort" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TG_RG_Resistance_thld-Kohm" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TG_RG_Resistance_thld-Kohm" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_TG_RG_Resistance_thld-Kohm" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.StorageService.{i}.NetworkServer.NetworkProtocolAuthReq" elementDefinition="InternetGatewayDevice.Services.StorageService.{i}.NetworkServer.NetworkProtocolAuthReq" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.AllowPiggybackEvents" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MGCP.AllowPiggybackEvents" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.RootApMode" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.RootApMode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.RootApMode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.AuthPassword" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.H323.AuthPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.BSSID" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.BSSID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.BSSID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DownloadDiagnostics.IPAddressUsed" elementDefinition="InternetGatewayDevice.DownloadDiagnostics.IPAddressUsed" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DownloadDiagnostics.IPAddressUsed" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.IfName" elementDefinition="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.IfName" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.IfName" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddressNotificationLimit" elementDefinition="InternetGatewayDevice.ManagementServer.UDPConnectionRequestAddressNotificationLimit" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.SentDHCPOption.{i}.Enable" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.DHCPClient.SentDHCPOption.{i}.Enable" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.TransmitSilenceSuppression" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Codec.TransmitSilenceSuppression" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MaxSessions" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.MaxSessions" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_IGMPCfg.IgmpVer" elementDefinition="InternetGatewayDevice.X_ALU-COM_IGMPCfg.IgmpVer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_IGMPCfg.IgmpVer" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.UDPEchoConfig.TimeLastPacketReceived" elementDefinition="InternetGatewayDevice.UDPEchoConfig.TimeLastPacketReceived" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.FaxAndModemRedundancy" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.RTP.Redundancy.FaxAndModemRedundancy" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.Codecs.{i}.BitRate" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.Capabilities.Codecs.{i}.BitRate" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Location_Data" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Location_Data" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.Location_Data" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.variableRetrievalEnabled" elementDefinition="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.variableRetrievalEnabled" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_EthOamIEEE8023ahCfg.variableRetrievalEnabled" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_DC_Voltage_Ring_Ground-Volt" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_DC_Voltage_Ring_Ground-Volt" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_DC_Voltage_Ring_Ground-Volt" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPRelay" elementDefinition="InternetGatewayDevice.LANDevice.{i}.LANHostConfigManagement.DHCPRelay" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SSID" elementDefinition="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SSID" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SSID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.NetMonitorDiagnostics.Timerinterval" elementDefinition="InternetGatewayDevice.NetMonitorDiagnostics.Timerinterval" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.NetMonitorDiagnostics.Timerinterval" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACAddressFilterList" elementDefinition="InternetGatewayDevice.Layer2Bridging.Filter.{i}.DestMACAddressFilterList" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MiniClassPrompt" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MiniClassPrompt" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MiniClassPrompt" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MaxLenRule" elementDefinition="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MaxLenRule" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.DeviceInfo.X_ALU-COM_ServiceManage.PasswordRule.MaxLenRule" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.InterfaceReference" elementDefinition="InternetGatewayDevice.Layer2Bridging.AvailableInterface.{i}.InterfaceReference" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize" elementDefinition="InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.Tr69Trusted" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.Tr69Trusted" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.WANIPConnection.{i}.X_ALU-COM_WanAccessCfg.Tr69Trusted" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.BandwidthIngress" elementDefinition="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.BandwidthIngress" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.X_ALU-COM_CommunityWifi.BandwidthIngress" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_Authentication.WebAccount.PresetPassword" elementDefinition="InternetGatewayDevice.X_Authentication.WebAccount.PresetPassword" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_Authentication.WebAccount.PresetPassword" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.UAPSDSupported" elementDefinition="InternetGatewayDevice.LANDevice.{i}.WLANConfiguration.{i}.UAPSDSupported" writable="true" monitoringLevel="RELEVANT" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.PacketsLost" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.Line.{i}.Stats.PacketsLost" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.X_ALU-COM_Wifi.ServiceID" elementDefinition="InternetGatewayDevice.X_ALU-COM_Wifi.ServiceID" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_Wifi.ServiceID" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTGatewayIDFormat" elementDefinition="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTGatewayIDFormat" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.X_ALU-COM_SmartHome.IotGWCtrl.IoTGatewayIDFormat" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.ManufacturerInfo.SoftwareVersion" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.ManufacturerInfo.SoftwareVersion" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_USBDongleInterfaceConfig.ManufacturerInfo.SoftwareVersion" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_CT-COM_WANGponLinkConfig.Mode" elementDefinition="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_CT-COM_WANGponLinkConfig.Mode" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.WANConnectionDevice.{i}.X_CT-COM_WANGponLinkConfig.Mode" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Stats.BytesSent" elementDefinition="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Stats.BytesSent" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.WANDevice.{i}.X_ALU-COM_LTEInterfaceConfig.Stats.BytesSent" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.QueueManagement.DefaultPolicer" elementDefinition="InternetGatewayDevice.QueueManagement.DefaultPolicer" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.ManagementServer.SupportedConnReqMethods" elementDefinition="InternetGatewayDevice.ManagementServer.SupportedConnReqMethods" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_AC_Voltage_Tip_Ground-Volt" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_AC_Voltage_Tip_Ground-Volt" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false">
        <definition name="InternetGatewayDevice.Services.VoiceService.{i}.PhyInterface.{i}.Tests.X_ALU-COM_MDT_AC_Voltage_Tip_Ground-Volt" description="" dataType="STRING" writable="true"/>
    </parameters>
    <parameters name="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.InboundAuth" elementDefinition="InternetGatewayDevice.Services.VoiceService.{i}.VoiceProfile.{i}.SIP.InboundAuth" writable="true" monitoringLevel="REQUESTONLY" simpleDiscovery="false"/>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.DownloadDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="Download Diagnostics" subType="DOWNLOADSPEED">
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.DSCP" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.DownloadURL" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.Interface" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.DownloadDiagnostics.EthernetPriority" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TotalBytesReceived"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.BOMTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TestBytesReceived"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.TCPOpenRequestTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.ROMTime"/>
        <returnParameterNames name="InternetGatewayDevice.DownloadDiagnostics.EOMTime"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.IPPingDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="IP Ping Diagnostics" subType="IPPING">
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.DSCP" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.Host" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.Interface" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.DataBlockSize" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.Timeout" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.IPPingDiagnostics.NumberOfRepetitions" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.MaximumResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.MinimumResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.FailureCount"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.SuccessCount"/>
        <returnParameterNames name="InternetGatewayDevice.IPPingDiagnostics.AverageResponseTime"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.TraceRouteDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="TraceRoute Diagnostics" subType="TRACEROUTE">
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.Host" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.MaxHopCount" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.Interface" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.NumberOfTries" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.DSCP" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.DataBlockSize" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.TraceRouteDiagnostics.Timeout" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.TraceRouteDiagnostics.RouteHopsNumberOfEntries"/>
        <returnParameterNames name="InternetGatewayDevice.TraceRouteDiagnostics.ResponseTime"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.UploadDiagnostics.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="Upload Diagnostics" subType="UPLOADSPEED">
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.DSCP" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.EthernetPriority" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.UploadURL" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.Interface" mandatory="false"/>
        <diagnosticParameters name="InternetGatewayDevice.UploadDiagnostics.TestFileLength" mandatory="false"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.BOMTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.EOMTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.TCPOpenRequestTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.TotalBytesSent"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.TCPOpenResponseTime"/>
        <returnParameterNames name="InternetGatewayDevice.UploadDiagnostics.ROMTime"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelSupportedDiagnosticOperation triggerParameterName="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.DiagnosticsState" triggerParameterFriendlyName="##acs.diagnostic_state##" name="WiFi Survey" description="" subType="WIFISURVEY" wifiChannelOption="ALLCHANNELS" wifiChannelOption5G="ALLCHANNELS">
        <returnParameterNames name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.BSSID"/>
        <returnParameterNames name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SignalStrength"/>
        <returnParameterNames name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.OperatingChannelBandwidth"/>
        <returnParameterNames name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SSID"/>
        <returnParameterNames name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.SecurityModeEnabled"/>
        <returnParameterNames name="InternetGatewayDevice.X_ALU-COM_NeighboringWiFiDiagnostic.Result.{i}.Channel"/>
    </deviceModelSupportedDiagnosticOperation>
    <deviceModelNetworkInterfaces isWAN="false" type="Ethernet" name="Ethernet 3" description="network interface definition">
        <properties name="Port Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.3.Stats.BytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.3.MACAddress" parameterType="MAC_ADDRESS"/>
        <properties name="Port Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.3.Status" parameterType="OTHER"/>
        <properties name="Port Bytes sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.3.Stats.BytesSent" parameterType="BYTES_SENT"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="Ethernet" name="Ethernet 2" description="network interface definition">
        <properties name="Port Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.Stats.BytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.MACAddress" parameterType="MAC_ADDRESS"/>
        <properties name="Port Bytes sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.Stats.BytesSent" parameterType="BYTES_SENT"/>
        <properties name="Port Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.2.Status" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 5" description="network interface definition">
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Status" parameterType="OTHER"/>
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.BSSID" parameterType="OTHER"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.SSID" parameterType="OTHER"/>
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.TotalBytesReceived" parameterType="OTHER"/>
        <properties name="WiFi Channel" category="CHANNEL" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Channel" parameterType="OTHER"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.TotalBytesSent" parameterType="OTHER"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.5.Enable" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 3" description="network interface definition">
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.3.BSSID" parameterType="OTHER"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.3.TotalBytesSent" parameterType="BYTES_SENT"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.3.Enable" parameterType="OTHER"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.3.SSID" parameterType="SSID"/>
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.3.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.3.Status" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 1" description="network interface definition">
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Enable" parameterType="OTHER"/>
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.BSSID" parameterType="OTHER"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.SSID" parameterType="OTHER"/>
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.TotalBytesReceived" parameterType="OTHER"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.TotalBytesSent" parameterType="OTHER"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Status" parameterType="OTHER"/>
        <properties name="WiFi Channel" category="CHANNEL" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.1.Channel" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 2" description="network interface definition">
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Status" parameterType="OTHER"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.Enable" parameterType="OTHER"/>
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.BSSID" parameterType="OTHER"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.TotalBytesSent" parameterType="BYTES_SENT"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.2.SSID" parameterType="SSID"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 8" description="network interface definition">
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.8.Enable" parameterType="OTHER"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.8.TotalBytesSent" parameterType="BYTES_SENT"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.8.SSID" parameterType="SSID"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.8.Status" parameterType="OTHER"/>
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.8.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.8.BSSID" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 7" description="network interface definition">
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.7.Status" parameterType="OTHER"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.7.SSID" parameterType="SSID"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.7.Enable" parameterType="OTHER"/>
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.7.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.7.BSSID" parameterType="OTHER"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.7.TotalBytesSent" parameterType="BYTES_SENT"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 6" description="network interface definition">
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.6.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.6.TotalBytesSent" parameterType="BYTES_SENT"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.6.SSID" parameterType="SSID"/>
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.6.Enable" parameterType="OTHER"/>
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.6.BSSID" parameterType="OTHER"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.6.Status" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="Ethernet" name="Ethernet 1" description="network interface definition">
        <properties name="MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.MACAddress" parameterType="MAC_ADDRESS"/>
        <properties name="Port Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.Stats.BytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Port Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.Status" parameterType="OTHER"/>
        <properties name="Port Bytes sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.1.Stats.BytesSent" parameterType="BYTES_SENT"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="Ethernet" name="Ethernet 4" description="network interface definition">
        <properties name="Port Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.4.Stats.BytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Port Bytes sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.4.Stats.BytesSent" parameterType="BYTES_SENT"/>
        <properties name="MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.4.MACAddress" parameterType="MAC_ADDRESS"/>
        <properties name="Port Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.LANEthernetInterfaceConfig.4.Status" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
    <deviceModelNetworkInterfaces isWAN="false" type="WIFI" name="Wifi 4" description="network interface definition">
        <properties name="Wifi Enabled" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.4.Enable" parameterType="OTHER"/>
        <properties name="Wifi Bytes Sent" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.4.TotalBytesSent" parameterType="BYTES_SENT"/>
        <properties name="Wifi MACAddress" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.4.BSSID" parameterType="OTHER"/>
        <properties name="Wifi SSID" category="ADDRESS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.4.SSID" parameterType="SSID"/>
        <properties name="Wifi Bytes Received" category="TRAFFIC" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.4.TotalBytesReceived" parameterType="BYTES_RECEIVED"/>
        <properties name="Wifi Status" category="STATUS" parameter="InternetGatewayDevice.LANDevice.1.WLANConfiguration.4.Status" parameterType="OTHER"/>
    </deviceModelNetworkInterfaces>
</DeviceModel>
