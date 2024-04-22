<!-- permalink: ab010c3705498311e5468321e0fd6ee8 DO NOT DELETE OR EDIT THIS LINE -->
# Swift Macros

Disclaimer: This is not definitive, just my understanding.

### Macro Types
* Freestanding Expression macro
	* can basically do `let a = #macroName(args)`
	* Declaration
		* example declaration keyword: `@freestanding(declaration, names: named(MyClass))`
			* (yanked directly from the examples - unsure if `names` is required, but it kinda seems like it is)
		* Generates [`[DeclSyntax]`](https://swiftpackageindex.com/apple/swift-syntax/510.0.1/documentation/swiftsyntax/declsyntax)
	* Expression
		* example declaration keyword: `@freestanding(expression)`
		* Generates [`ExprSyntax`](https://swiftpackageindex.com/apple/swift-syntax/510.0.1/documentation/swiftsyntax/exprsyntax)

* Attached Macros
	* Accessor
		* Adds accessors (like `get`, `set`, `didSet`, `willSet`, and more complex ones too (see docs)
		* example declaration keyword: `@attached(accessor)`
		* Generates [`[AccessorDeclSyntax]`](https://swiftpackageindex.com/apple/swift-syntax/510.0.1/documentation/swiftsyntax/accessordeclsyntax)
	* CodeItem
		* could not find example declaration keyword example
		* Generates [`[CodeBlockItemSyntax]`](https://swiftpackageindex.com/apple/swift-syntax/510.0.1/documentation/swiftsyntax/codeblockitemsyntax)
	* Extension
		* example declaration keyword: `@attached(extension, conformances: Equatable)`
			* (again yanked from examples. conformances doesn't look explicitly required, but the one time it's omitted there's an alternative argument provided)
		* Generates [`[ExtensionDeclSyntax]`](https://swiftpackageindex.com/apple/swift-syntax/510.0.1/documentation/swiftsyntax/extensiondeclsyntax)
	* Member
		* Can add *members* to the declaration it's attached to
		* example declaration keyword:

			```swift
			@attached(
			  member,
			  names: named(Storage),
			  named(_storage),
			  named(_registrar),
			  named(addObserver),
			  named(removeObserver),
			  named(withTransaction)
			)
			```

			* appears as if `names` can take one or more arguments
		* Generates [`[DeclSyntax]`](https://swiftpackageindex.com/apple/swift-syntax/510.0.1/documentation/swiftsyntax/declsyntax)
		* I believe this means something like

			```swift
			@MahMancro
			class Foo {}
			```

			Can expand to something like 

			```swift
			class Foo {
				var bar: Int
				func baz () {}
			}
			```

	* MemberAttribute
		* Can add *attributes* to members inside the declaration it's attached to
		* example declaration keyword: `@attached(memberAttribute)`
		* Generates [`[AttributeSyntax]`](https://swiftpackageindex.com/apple/swift-syntax/510.0.1/documentation/swiftsyntax/attributesyntax)
		* I believe this means something like

			```swift
			@MahMancro
			class Foo {
				var bar: Int
				var baz: String
			}
			```

			Can expand to something like 

			```swift
			class Foo {
				@MahSubMancro
				var bar: Int
				@MahSubMancro
				var bax: String
			}
			```

	* Peer
		* Can add "peer" declarations alongside its attached declaration
		* examples of declaration keyword:

			```swift
			@attached(peer, names: overloaded)
			@attached(peer, names: suffixed(_peer))
			```

		* Generates [`[DeclSyntax]`](https://swiftpackageindex.com/apple/swift-syntax/510.0.1/documentation/swiftsyntax/declsyntax)
		* I believe this means something like

			```swift
			@MahMancro
			let url = URL(string: "https://the-google.com/")
			```

			Can expand to something like 

			```swift
			let url = URL(string: "https://the-google.com/")
			let url_request = URLRequest(url: url)
			```

references:

* [swift ast](https://swift-ast-explorer.com)
* [swift-syntax docs](https://swiftpackageindex.com/apple/swift-syntax/510.0.1/documentation/swiftsyntax)
* [macro-examples](https://github.com/apple/swift-syntax/tree/4824d4d0ee6b733f8fb87016b165e55c37127190/Examples/Sources/MacroExamples) (dated 4/21/24)
	* [macro protocol headers](https://github.com/apple/swift-syntax/tree/4824d4d0ee6b733f8fb87016b165e55c37127190/Sources/SwiftSyntaxMacros/MacroProtocols) (dated 4/21/24)
* [Mah Man](https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExaDlqc21tazZrZ2N1OXE3b2ttaDFremR2djduZHdua2FkYW56Y2QzdiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/qPVzemjFi150Q/giphy.gif)
