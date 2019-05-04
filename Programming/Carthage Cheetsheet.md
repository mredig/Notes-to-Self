<!-- permalink: 449862b9a85c3e7c360e9bb1299ed49b DO NOT DELETE OR EDIT THIS LINE -->
# Carthage Setup Cheatsheet

1. Create cartfile and add libraries
1. run `carthage update` (or `carthage bootstrap` if working from an existing project)
	* options:
		* `--platform`
			* `ios`, `tvos`, `macOS`, `watchos` (comma separated, no spaces if needing more than one)
		* `--cache-builds`
			* attempts to reuse existing builds of frameworks instead of rebuilding from scratch
1. You may need to wait for the build to finish to be able to add the frameworks to your Xcode project, but you may proceed with the following in general in the meantime
1. In Xcode, for each target, add a *Run Script* build phase
	1. **Suggestion**: rename the phase to something like `Run Script - Carthage`
	1. put the following in script portion:
		``` 
		/usr/local/bin/carthage copy-frameworks
		/usr/local/bin/carthage outdated --xcode-warnings
		```

	1. Use the following template (for iOS, modify appropriately for others), based off of the built framework name(s), and add the following entry to *Input Files* for each framework (you can find the built framework names by going to `Carthage/Build/*/[frameworksHere]` )
		* `$(SRCROOT)/Carthage/Build/iOS/[frameworkNameNoBrackets].framework`
	1. Use the following template and do the same for *Output Files*
		* `$(BUILT_PRODUCTS_DIR)/$(FRAMEWORKS_FOLDER_PATH)/[frameworkNameNoBrackets].framework`
1. In the *General* tab of the Xcode target, drag the frameworks from `Carthage/Build/[build platform]/[frameworksHere]`
1. (wait for `carthage update` to finish first) Build your project to make sure everything is working right




More information is available [here](https://github.com/Carthage/Carthage#getting-started).
