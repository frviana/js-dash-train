# Incognito DX ACS Dashboard

## WiFi 5Ghz Configuration Panel
### DeviceModel name="TP-Link_IGD_CABO"
### manufacturer="TP-Link_IGD_CABO"
### oui="5CA6E6,003192,005F67,3C846A,50D4F7,6032B1,60A4B7,6C5AB0,74DA88,84D81B,C006C3,C0C9E3,CC32E5,D807B6,D84732,E4C32A"
### productClass="IGD"
### objectModelDefinitions="InternetGatewayDevice:1.1"

## WiFi Panel javaScriptCode:
var dsc = require("deviceserviceconfiguration");

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
    parameter.value = "Mixed 11b & 11g";
  }
  if(parameter.value == "b, g, n") {
    parameter.value = "Mixed 11b, 11g & 11n";
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
      { systemName:"b, g", friendlyName: "Mixed 11b & 11g" },
      { systemName:"n", friendlyName: "11n Only" },
      { systemName:"b, g, n", friendlyName: "Mixed 11b, 11g & 11n" }
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
          if(value < 0 || value > 200)
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
              if(PasswordIndex < 1 && PasswordIndex > 4)
                throw "Key index must be between 1 and 4";
              cpeParameters.CurrentPasswordIndex.value = scriptParameters.CurrentPasswordIndex;
              cpeParameters.CurrentPasswordIndex.updated = true;
            } else {
              throw "Key index must be between 1 and 4";
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

            if (typeof scriptParameters.Password != 'undefined' && scriptParameters.Password !== null) {
              if(scriptParameters.Password.length < 8)
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