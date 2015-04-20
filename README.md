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

* It is better to commit everything (+ build locations)! This is because cordova app depends on plugins, and it can break if updated codes from plugins are bad (assuming the latest codes are UNSTABLE).

* If getting ERROR: spawn EACCES

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

* If Getting "SSL Certificate Error Alert"
`http://www.thomasmaximini.com/2015/01/23/getting-started-with-crosswalk-in-ionic.html`
