---
title:  "Configure Fiddler For Android and IOS"
author: "Saurabh Londhe"
avatar: "img/authors/saurabh.jpg"
image: "img/fiddler-banner.png"
date:   2019-06-25
categories: [Network]
---

Fiddler is an HTTP debugging proxy server application originally written by Eric Lawrence, formerly a program manager on the Internet Explorer development team at Microsoft.

### Configure Fiddler for remote Android and IOS devices

At Fiddler side
-   For activating remote devices traffic to go through fiddler we need to enable it. Can be done by navigating to
    ```Tools > Options > Connections > Allow remote computers to connect```

-   `Allow remote computers to connect` Enable the checkbox and to reflect Fiddler need to restart

-   Note the port of proxy server which is `8888` by default

![Fiddler connections](img/fiddler/connections.png)

-   Hover on right corner on online tab so that server's ip will be shown

    ![Fiddler IP](img/fiddler/OnlineTooltip.png)

---

At Android side
-   Connent to the same network.
-   Open WIFI settings for modifying the connection
    -   Touch and hold wifi name and select `Manage network settings`

    <img src="img/fiddler/android-1.png" class="inner-img">

    -   Choose `Show advance options`
    -   At Proxy settings choose Manual

    <img src="img/fiddler/android-2.png" class="inner-img">

    -   Enter Fiddler's IP address at `Proxy host name`
    -   Enter `Proxy Port` i.e. `8888` 
    -   Save the settings

    <img src="img/fiddler/android-3.png" class="inner-img">

    -   Now to Varify connection please hit the url [ipv4.fiddler:8888](http://ipv4.fiddler:8888) in Android browser. You will get web page as below
    
    <img src="img/fiddler/DownloadFiddlerRootCert.png" class="inner-img">

    -   Download and install Certificate from storage. This certificate helps to decrypt the requests

---

At IOS side

-   Connent to the same network.
-   Open WIFI settings for modifying the connection
    -   Touch and open WIFI info
    -   Scroll down and choose `Configure Proxy`

    <img src="img/fiddler/ios-1.png" class="inner-img">

    -   Enter Fiddler's IP address at `Server`
    -   Enter `Port` i.e. `8888` 
    -   Save the settings

    <img src="img/fiddler/ios-2.png" class="inner-img">

    -   Now to Varify connection please hit the url [ipv4.fiddler:8888](http://ipv4.fiddler:8888) in Android browser. You will get web page as below
    
    <img src="img/fiddler/DownloadFiddlerRootCert.png" class="inner-img">

    -   Download and install Certificate. This certificate helps to decrypt the requests
    - On IOS you'll need to enable the certificate by navigating to
    `General > About > ertificate Trust Settings`

    <img src="img/fiddler/ios-cert.png" class="inner-img">
