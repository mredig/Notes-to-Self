<!-- permalink: 449862b9a85c3e7c360e9bb1299ed49b DO NOT DELETE OR EDIT THIS LINE -->
# Carthage Setup Cheatsheet


### Setup cheats
1. Create cartfile and add libraries
1. run `carthage update` (or `carthage bootstrap` if working from an existing project)
	* options:
		* `--platform`
			* `ios`, `tvos`, `macOS`, `watchos` (comma separated, no spaces if needing more than one)
		* `--cache-builds`
			* attempts to reuse existing builds of frameworks instead of rebuilding from scratch
		* `--no-use-binaries`
			* disables downloading pre built binaries. This makes running it a lot slower, but resolves issues with debugging output not working in Xcode. 
1. You may need to wait for the build to finish to be able to add the frameworks to your Xcode project, but you may proceed with the following in general in the meantime
1. if you are doing iOS, these are your instructions (for macOS skip to the next step):
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
	1. In the *General* tab of the Xcode target, drag the frameworks from `Carthage/Build/[build platform]/[frameworksHere]` to the *Linked Frameworks and Libraries* section
		* You should not need to copy files
	1. (wait for `carthage update` to finish first) Build your project to make sure everything is working right
1. for macOS, simply drop the built frameworks from the `Carthage/Build` folder into the macOS build target's `Embedded Binaries`.

### Supporting Carthage
1. Double check permission levels
1. Make sure to share you set your build scheme to `Shared`
1. run `carthage build --no-skip-current` in the project directory to confirm everything builds fine

More information is available [here](https://github.com/Carthage/Carthage#getting-started).
