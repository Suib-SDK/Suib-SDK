# Mopub Mediation Integration Guide

## <a name="start">Before You Start</a>  

* Support Native, Banner, Interstital and Rewarded Video.
* Support API 14(Android 4.0 or later).
* The Mopub account is needed. 
* Make sure you have correctly integrated Mopub Rewarded Video or Interstitial(Fullscreen) or Banner or Native Mediation into your application.
* Please make sure you have get your own slot id for test. 
* [Download the latest Zcoup SDK](https://github.com/zero-sdk/Android_SDK/blob/master/ZcoupSDK.zip)
* [Download the Zcoup Adapter for Mopub](https://github.com/zero-sdk/Android_SDK/blob/master/ZcoupSDK_Adapter-For-Mopub.zip)

## <a name="Docking">Intergation</a>

### Step 1: Integrate Mopub SDK    

> If you haven't already, make sure you've integrate MoPub SDK.
> Log on to the Mopub website:[MoPub Platform](https://app.mopub.com/account/login)


### Step 2: Integrate Zcoup SDK

* Detail of Zcoup SDK

    | jar name | jar function |
    | --- | --- |
    | zcoup_base_xx.jar        | for banner\fullscreem\native ads |
    | zcoup_video_xx.jar       | RewardedVideo function |
    | zcoup_imageloader_xx.jar | Imageloader function |

* Add the needed jars to your module's libs/
* Update the module's build.gradle as follows

    ```groovy
    dependencies {
    	   implementation files('libs/zcoup_base_xx.jar')
    	   implementation files('libs/zcoup_video_xx.jar')
    	   implementation files('libs/zcoup_imageloader_xx.jar')
    }
    ```

* Update the AndroidManifest.xml

    ```xml
    <!--for non google play Ad-->
    <activity android:name="suib.base.view.InnerWebViewActivity" />
    
    <!--for RewardedVideo-->
    <activity
        android:name="suib.video.view.RewardedVideoActivity"
        android:configChanges="keyboard|keyboardHidden|orientation|screenLayout|uiMode|screenSize|smallestScreenSize" />
    
    <!-- for Interstitial -->
    <activity android:name="suib.base.view.InterstitialActivity" />  
    
    ```

### Step 3: Integrate the adapter

* Details of the adapter

    | file name | file function |
    | --- | --- |
    | ZCAdapterBanner.java | for banner ads |
    | ZCAdapterInterstitial.java | for fullscreen ads |
    | ZCAdapterNative.java | for native ads |
    | ZCAdapterRewardedVideo.java | for RrewardedVideo ads |
    | ZCHelper.java | Support above function. |

* Copy the needed adapter files into your project source folder, like follows:

    ![image](https://user-images.githubusercontent.com/15087458/50625657-74aaaf00-0f64-11e9-848a-c4a33a44d7b1.png)

    
### Step 4: MoPub Configuration

* Create apps and ad unit id in Mopub console

    ![image](https://user-images.githubusercontent.com/15087458/50625923-1ed70680-0f66-11e9-81bd-dee2b5abbecd.png)

* Create Zcoup network
    
    ![image](https://user-images.githubusercontent.com/15087458/50625949-5180ff00-0f66-11e9-8ba9-7485c8a426d6.png)

* Realize the ad unit setup for network

>  Get the detail class name of adapter file in your project，like follows:

| ad type | full class name |
| --- | --- |
| Banner ad unit     | suib.mediation.mopub.CTAdapterBanner |
| FullScreen ad unit | suib.mediation.mopub.CTAdapterFullScreen |
| Native ad unit     | suib.mediation.mopub.CTAdapterNative |
| RewardedVideo ad unit | suib.mediation.mopub.CTAdapterRewardVideo |

> For each unit, add a JSON object:  **{"CT_SLOTID":"your slotID"}**
  
  ![image](https://user-images.githubusercontent.com/15087458/50625736-eb47ac80-0f64-11e9-9e6a-04ca14b33635.png)









