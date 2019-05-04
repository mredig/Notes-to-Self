# Xcode Tips


### Build number
* Auto increment build number with every build
	* Add a `Run Script` build phase with the following script:
		```
		#!/bin/bash
		bN=$(/usr/libexec/PlistBuddy -c "Print CFBundleVersion" "$INFOPLIST_FILE")
		bN=$((bN += 1))
		bN=$(printf "%d" $bN)
		/usr/libexec/PlistBuddy -c "Set :CFBundleVersion $bN" "$INFOPLIST_FILE"
		```
	* *Suggested*: rename the `Run Script` phase to `Increment Build Script`


### Formatting
* Swiftlint
	1. Install swiftlint
		* `brew install swiftlint` ([alternatives exist](https://github.com/realm/SwiftLint#installation) for installing swiftlint)
	1. Add a `Run Script` build phase with the following script:
		```
		if which swiftlint >/dev/null; then
			swiftlint
		else
			echo "warning: SwiftLint not installed, download from https://github.com/realm/SwiftLint"
		fi
		```

### Miscellaneous
* Hold `` or `Option` while hovering over a bracket with your mouse to see the scope highlighted
* Change from stupid *spaces* to smart *tabs* for indentation by opening *Preferences*->*Text Editing*, choose the *Indentation* option and choose `Tabs` from the *Prefer indent using:* dropdown.
