<!-- permalink: 6632506ec33abcc86e04a3ab7f4d3a47 DO NOT DELETE OR EDIT THIS LINE -->
# LLDB on CLI

1. Build with debug symbols
1. run `lldb ./path/to/exe`
	* for spm, it'll be `swift build` followed by `lldb .build/debug/<your exe name>
	* for spm tests, you can run `lldb .build/debug/<YourPackageName>PackageTests.xctest`
1. To set breakpoints
	* `breakpoint set --file FileName.swift --line 42`
1. `run`

