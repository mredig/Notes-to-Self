<!-- permalink: d5cfede3389c6db892e35ddfcd909d60 DO NOT DELETE OR EDIT THIS LINE -->
# Swift Regex Reference

* Labelled match

	```swift
	let fooRegex = /foo="(?<fooValue>.*)"/

	let string = """
	foo="bar"
	"""

	let match = string.matches(of: fooRegex).first!

	print("match: \(match.output.fooValue)") // prints 'bar'
	```
