# Trace ndc - Network Daemon Controller


## Requirements


### startSoftApWithConfig



FILE --> frameworks/opt/net/wifi/service/java/com/android/server/wifi/WifiStateMachine.java
@@@@@        startSoftApWithConfig  __call startAccessPoint


### startAccessPoint

ndc softap set ...
FILE  --> frameworks/base/services/core/java/com/android/server/NetworkManagementService.java
@@@@@       startAccessPoint  __call  SoftapController::setSoftap


* [Android netd ndc](http://blog.chinaunix.net/uid-23381466-id-5112474.html)
* [NativeDaemonConnector](http://gaozhipeng.me/posts/nativedaemonconnector_source_code/)




```cpp
public void startAccessPoint(
        WifiConfiguration wifiConfig, String wlanIface) {
    mContext.enforceCallingOrSelfPermission(CONNECTIVITY_INTERNAL, TAG);
    try {
        wifiFirmwareReload(wlanIface, "AP");
        if (wifiConfig == null) {
            mConnector.execute("softap", "set", wlanIface);
        } else {
            mConnector.execute("softap", "set", wlanIface, wifiConfig.SSID,
                               "broadcast", Integer.toString(wifiConfig.apChannel),
                               getSecurityType(wifiConfig),
                               new SensitiveArg(wifiConfig.preSharedKey));
        }
        mConnector.execute("softap", "startap");
    } catch (NativeDaemonConnectorException e) {
        throw e.rethrowAsParcelableException();
    }
}
```



## end of file




