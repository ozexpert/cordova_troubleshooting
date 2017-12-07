Cordova Troubleshooting
=======================

Just documenting some troubles for Cordova


* When building cordova for ios and is appending .xcodeproj twice

    http://stackoverflow.com/questions/20915395/phonegap-build-ios-exception-with-helloworld-application
    Open platforms/ios/cordova/build
    and then change to 
    
    XCODEPROJ=$( ls "$PROJECT_PATH" | grep --color=never .xcodeproj  )
    
* After "ionic start <project_name>" and adding platform "cordova platform add android"
  * Need to change app name in config.xml / AndroidManifest.xml 
  * Change platforms/android/src/com/ionicframework/ozcordova811643/CordovaApp.java to <your_app_name>.java and open that file and change the class name as well
  * This is same for renaming the application


* Error handling (client side)

```
    window.onerror = function(msg, url, line, col, error) {
       // Note that col & error are new to the HTML 5 spec and may not be 
       // supported in every browser.  It worked for me in Chrome.
       var extra = !col ? '' : '\ncolumn: ' + col;
       extra += !error ? '' : '\nerror: ' + error;
    
       // You can view the information in an alert to see things working like this:
       alert("Error: " + msg + "\nurl: " + url + "\nline: " + line + extra);
    
       // TODO: Report this error via ajax so you can keep track
       //       of what pages have JS issues
    
       var suppressErrorAlert = true;
       // If you return true, then error alerts (like in older versions of 
       // Internet Explorer) will be suppressed.
       return suppressErrorAlert;
    };
```

* It is better to commit everything (+ build locations)! This is because cordova app depends on plugins, and it can break if updated codes from plugins are bad (assuming the latest codes are UNSTABLE).

* If getting ERROR: spawn EACCES

```
    Youngs-MacBook-Pro:oneverse youngpark$ cordova prepare
    Running command: /Users/youngpark/CIF/oneverse/hooks/after_prepare/010_add_platform_class.js /Users/youngpark/CIF/oneverse
    Error: spawn EACCES
        at exports._errnoException (util.js:746:11)
        at ChildProcess.spawn (child_process.js:1155:11)
        at Object.exports.spawn (child_process.js:988:9)
        at Object.exports.spawn (/usr/local/lib/node_modules/cordova/node_modules/cordova-lib/src/cordova/superspawn.js:100:31)
        at runScriptViaChildProcessSpawn (/usr/local/lib/node_modules/cordova/node_modules/cordova-lib/src/hooks/HooksRunner.js:188:23)
        at runScript (/usr/local/lib/node_modules/cordova/node_modules/cordova-lib/src/hooks/HooksRunner.js:131:16)
        at /usr/local/lib/node_modules/cordova/node_modules/cordova-lib/src/hooks/HooksRunner.js:114:20
        at _fulfilled (/usr/local/lib/node_modules/cordova/node_modules/q/q.js:787:54)
        at self.promiseDispatch.done (/usr/local/lib/node_modules/cordova/node_modules/q/q.js:816:30)
        at Promise.promise.promiseDispatch (/usr/local/lib/node_modules/cordova/node_modules/q/q.js:749:13)
    Youngs-MacBook-Pro:oneverse youngpark$ ls -al /usr/local/lib/node_modules
    total 0
    drwxr-xr-x   8 24561   wheel  272 Apr  2 10:16 .
    drwxrwxr-x   4 24561   admin  136 Feb  6 12:19 ..
    drwxr-xr-x  18 nobody  staff  612 Mar 23 13:50 cordova
    drwxr-xr-x  11 nobody  staff  374 Mar 23 16:54 gulp
    drwxr-xr-x  13 nobody  staff  442 Mar 28 21:27 ionic
    drwxr-xr-x  17 nobody  staff  578 Apr  2 10:16 ios-deploy
    drwxr-xr-x  26 65534   staff  884 Mar 23 13:12 npm
    drwxr-xr-x  12 nobody  staff  408 Mar 23 16:54 sass
    Youngs-MacBook-Pro:oneverse youngpark$ ls -al /usr/local/lib/
    total 0
    drwxrwxr-x  4 24561  admin  136 Feb  6 12:19 .
    drwxr-xr-x  7 502    staff  238 Mar 28 19:02 ..
    drwxr-xr-x  3 24561  wheel  102 Feb  6 12:19 dtrace
    drwxr-xr-x  8 24561  wheel  272 Apr  2 10:16 node_modules
    Youngs-MacBook-Pro:oneverse youngpark$ chmod +x /Users/youngpark/CIF/oneverse/hooks/after_prepare/010_add_platform_class.js 
```

* If Getting "SSL Certificate Error Alert"
`http://www.thomasmaximini.com/2015/01/23/getting-started-with-crosswalk-in-ionic.html`

* If getting below error when compiling, then DO `cordova platform update <platform>`

```
    module.js:338
        throw err;
              ^
    Error: Cannot find module 'q'
        at Function.Module._resolveFilename (module.js:336:15)
        at Function.Module._load (module.js:278:25)
        at Module.require (module.js:365:17)
        at require (module.js:384:17)
        at Object.<anonymous> (/Users/youngpark/CIF/oneverse/platforms/android/cordova/lib/spawn.js:23:15)
        at Module._compile (module.js:460:26)
        at Object.Module._extensions..js (module.js:478:10)
        at Module.load (module.js:355:32)
        at Function.Module._load (module.js:310:12)
        at Module.require (module.js:365:17)
```

* If getting "Application Error: Connection to server was unsuccessful to “www/assets/index.html”" when starting up apps:

    https://www.robertkehoe.com/2013/01/fix-for-phonegap-connection-to-server-was-unsuccessful/

* If getting `You have not accepted the license agreements of the following SDK components: [Android SDK Build-Tools 24, Android SDK Platform 24]`

* If getting `Error: spawn EACCESS` for android

    http://randomitstuff.com/2017/06/16/error-spawn-eacces-when-building-for-android-on-cordova/

```
android update sdk --no-ui --filter build-tools-24.0.0,android-24,extra-android-m2repository
```

# IOS

* If getting ExecutableKey error

    http://stackoverflow.com/questions/32096130/unexpected-cfbundleexecutable-key

# Useful Tip

* Using multiple Github account on single pc

    http://code.tutsplus.com/tutorials/quick-tip-how-to-work-with-github-and-multiple-accounts--net-22574
