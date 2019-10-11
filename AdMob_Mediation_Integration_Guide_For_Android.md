# AdMob Mediation Integration Guide

This guide instructs you step-by-step on how to set Suib live as an Ad Network on the Admob Mediation platform.

Currently we support Rewarded Video, Banner and Interstitial for mediation.

### Before You Start

- Make sure you have creat an application and ad slotIds on the our Platform.
- [Download the latest Suib SDK](https://github.com/Suib-SDK/Suib-SDK/blob/master/SuibSDK.zip)
- [Download the Suib Adapter for Mopub](https://github.com/Suib-SDK/Suib-SDK/blob/master/SuibSDK_Adapter-For-Admob.zip)


### Step 1: Integrate Suib SDK and Adapter

* Detail of Suib SDK

    | jar name | jar function |
    | --- | --- |
    | suib_base_xx.jar        | for banner\fullscreem\native ads |
    | suib_video_xx.jar       | RewardedVideo function |
    | suib_imageloader_xx.jar | Imageloader function |

* Add the needed jars to your module's libs/
* Update the module's build.gradle as follows

 ```
    dependencies {
       implementation files('libs/suib_base_xx.jar')
       implementation files('libs/suib_video_xx.jar')
       implementation files('libs/suib_imageloader_xx.jar')
    }
 ```

* Update the AndroidManifest.xml


 ```xml
	<!--Necessary Permissions-->
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />

  <!--for RewardedVideo-->
  <activity
	android:name="com.suib.video.view.RewardedVideoActivity"
	android:configChanges="keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize" />
	
 <!-- for Interstitial -->
<activity android:name="com.suib.base.view.InterstitialActivity" /> 
    	
	<!-- Necessary -->
	<activity android:name="com.suib.base.view.InnerWebViewActivity" />

	<provider
            android:authorities="${applicationId}.xxprovider"
            android:name="com.suib.base.core.SuibProvider"
            android:exported="false"/>
	

	<!--If your targetSdkVersion is 28, you need update <application> as follows:-->
  	<application
    	...  	
        android:usesCleartextTraffic="true"
        ...>
        ...
    </application>
```


* Copy the needed adapter files into your project source folder, like follows:

    ![image](https://user-images.githubusercontent.com/15087458/50626675-898a4100-0f6a-11e9-815f-830ff0d72a55.png)

### Step 2: Create Mediation Group

![image](https://user-images.githubusercontent.com/20314643/34598723-6a3249e2-f229-11e7-96b8-0ba05840c957.png)

1.1 Choose the ad format and platform

Currently we support rewarded video and interstitial mediation for Android

![image](https://user-images.githubusercontent.com/20314643/34598771-abf82482-f229-11e7-8f5b-849a295461fa.png)

1.2 Select your targeting location, turn the status on and "add ad units"

![image](https://user-images.githubusercontent.com/20314643/34598876-34953cd0-f22a-11e7-9d76-f2610179dc99.png)

1.3 Select your application and ad units that you plan to integrate with Cloudmobi

![image](https://user-images.githubusercontent.com/20314643/34598969-da664082-f22a-11e7-9441-c6aca7cd93ba.png)

### step 3: Define Custom Events

”eCPM“ determines the order of the ad network to serve ads.

![image](https://user-images.githubusercontent.com/20314643/34599932-fab8e6c8-f22f-11e7-93df-37119420eb58.png)

![image](https://user-images.githubusercontent.com/20314643/34600140-f0e26a74-f230-11e7-9451-baaaf675b2ce.png)

### Step 4: Add Suib custom event in Admob console

![image](https://user-images.githubusercontent.com/20314643/34600301-c64459c0-f231-11e7-8ab5-67a61423e5ea.png)

(1) Class Names should match the ad formats in Suib -- for example, if you are integrating rewarded video ads, the full class name should be: 

 ```
    com.suib.mediation.admob.ZCustomEventRewardedVideo
 ```

(2) Parameter is the slot ID, you can get it from our operational staff

### Step 5. Add ProGuard Rules

```
    -dontoptimize
    -dontpreverify
    
    #for sdk
    -dontwarn com.suib.**
    -keep public class com.suib.**{*;}
    
    #for gaid
    -keep class **.AdvertisingIdClient$** { *; }
```
**Done!** You are now all set to deliver Cloudmobi Ads within your application!

For more details information about Custom Events in Admob Mediation, please click [here](https://developers.google.com/admob/android/custom-events)

