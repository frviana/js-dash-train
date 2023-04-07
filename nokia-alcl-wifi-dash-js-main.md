# Incognito DX ACS Dashboard

## WiFi 5Ghz Configuration Panel
### DeviceModel name="Nokia-ALCL-CaboNatal"
### manufacturer="Nokia-ALCL-CaboNatal"
### oui="184593,6CC63B,9075BC,E01FED,104738,549F06"
### productClass="G-2425G-A,G-140W-H,G-240W-G,G-1425G-A"
### objectModelDefinitions="InternetGatewayDevice:1.14 VoiceService:2.0 StorageService:1.2"

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
