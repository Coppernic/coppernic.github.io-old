Barcode scanning
===============
Context 
-----------
This application demonstrates how to scan a barcode on Coppernic device.

Trig a barcode
-------------------

There are 2 ways to trig a barcode reading:
- Remap a physical button to barcode scan function
- Send an intent

### Remap a physical button to barcode reading

In the settings, go to remap key & shortcuts (may change on different devices), then remap a key to SCAN or Barcode Scan (device dependent).

### Send an intent

```groovy
Intent scanIntent = new Intent();
scanIntent.setPackage(SERVICE_PACKAGE_NAME);
scanIntent.setAction(INTENT_ACTION_SCAN);
scanIntent.putExtra(KEY_PACKAGE, this.getPackageName());
ComponentName info = this.startService(scanIntent);
if (info != null) {
    // OK
} else {
    // Error
}
```

where

```groovy
private static final String SERVICE_PACKAGE_NAME = "fr.coppernic.service.cfive"; //cfive for C-five, ceight for C-eight cone for C-One
private static final String INTENT_ACTION_SCAN = "fr.coppernic.intent.action.SCAN";
private static final String KEY_PACKAGE = "package";
```

Get data read
------------------
Data read (and errors) are sent back with an intent. You need to declare a BroadcastReceiver to get it:

```groovy
private BroadcastReceiver scanResult = new BroadcastReceiver() {
    @Override
    public void onReceive(Context context, Intent intent) {
        if (intent.getAction().equals(ACTION_SCAN_SUCCESS)) {
            String dataRead = intent.getExtras().getString(BARCODE_DATA);
        } else if (intent.getAction().equals(ACTION_SCAN_ERROR)) {
            // Handle error
        }
    }
};
```

Where

```groovy
public final static String ACTION_SCAN_SUCCESS = "fr.coppernic.intent.scansuccess";
public final static String ACTION_SCAN_ERROR = "fr.coppernic.intent.scanfailed";
public final static String BARCODE_DATA = "BarcodeData";
```

This broadcast receiver needs to be registered:

```groovy
private void registerReceiver() {
    IntentFilter filter = new IntentFilter();
    filter.addAction(ACTION_SCAN_SUCCESS);
    filter.addAction(ACTION_SCAN_ERROR);
    registerReceiver(scanResult, filter);
}
```
For example in the onResume method of an Activity:

```groovy
@Override
protected void onResume() {
    super.onResume();
    registerReceiver();
}
```

And unregistered in the onPause for example:

```groovy
@Override
protected void onPause() {
     super.onPause();
     unregisterReceiver(scanResult);
}
```


