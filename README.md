cordova_troubleshooting
=======================

Just documenting some troubles for Cordova


* When building cordova for ios and is appending .xcodeproj twice

    http://stackoverflow.com/questions/20915395/phonegap-build-ios-exception-with-helloworld-application
    
* After "ionic start <project_name>" and adding platform "cordova platform add android"
  * Need to change app name in config.xml / AndroidManifest.xml 
  * Change platforms/android/src/com/ionicframework/ozcordova811643/CordovaApp.java to <your_app_name>.java and open that file and change the class name as well
  * This is same for renaming the application
