## Mac Fixes

### Fix: Uninstall Visual Studio for Mac

Microsoft description how to [uninstall VS](https://learn.microsoft.com/en-us/previous-versions/visualstudio/mac/uninstall?view=vsmac-2022)

To run script:
```bash
chmod +x ./uninstall-vs.sh
sudo ./uninstall-vs.sh
```

Modified script, can be run line by line:
```bash
#!/bin/sh

# Uninstall Visual Studio for Mac
echo "Uninstalling Visual Studio for Mac..."

sudo rm -rf "/Applications/Visual Studio.app"
rm -rf ~/Library/Caches/VisualStudio
rm -rf ~/Library/Preferences/VisualStudio
rm -rf "~/Library/Preferences/Visual Studio"
rm -rf ~/Library/Logs/VisualStudio
rm -rf ~/Library/VisualStudio
rm -rf ~/Library/Preferences/Xamarin/
rm -rf ~/Library/Developer/Xamarin

# Uninstall Xamarin.Android
echo "Uninstalling Xamarin.Android..."

sudo rm -rf /Developer/MonoDroid
rm -rf ~/Library/MonoAndroid
sudo pkgutil --forget com.xamarin.android.pkg
sudo rm -rf /Library/Frameworks/Xamarin.Android.framework


# Uninstall Xamarin.iOS
echo "Uninstalling Xamarin.iOS..."

rm -rf ~/Library/MonoTouch
sudo rm -rf /Library/Frameworks/Xamarin.iOS.framework
sudo rm -rf /Developer/MonoTouch
sudo pkgutil --forget com.xamarin.monotouch.pkg
sudo pkgutil --forget com.xamarin.xamarin-ios-build-host.pkg


# Uninstall Xamarin.Mac
echo "Uninstalling Xamarin.Mac..."

sudo rm -rf /Library/Frameworks/Xamarin.Mac.framework
rm -rf ~/Library/Xamarin.Mac


# Uninstall Workbooks and Inspector
echo "Uninstalling Workbooks and Inspector..."

sudo /Library/Frameworks/Xamarin.Interactive.framework/Versions/Current/uninstall


# Uninstall the Visual Studio for Mac Installer
echo "Uninstalling the Visual Studio for Mac Installer..."

rm -rf ~/Library/Caches/XamarinInstaller/
rm -rf ~/Library/Caches/VisualStudioInstaller/
rm -rf ~/Library/Logs/XamarinInstaller/
rm -rf ~/Library/Logs/VisualStudioInstaller/

# Uninstall the Xamarin Profiler
echo "Uninstalling the Xamarin Profiler..."

sudo rm -rf "/Applications/Xamarin Profiler.app"

echo "Finished Uninstallation process."
```
