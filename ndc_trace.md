# Trace ndc - Network Daemon Controller


## Requirements


show code



```
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




