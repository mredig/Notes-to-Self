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
