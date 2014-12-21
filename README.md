cordova_troubleshooting
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
