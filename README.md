
# conekta_tokenizer

A Flutter plugin that allows to create a [Conekta](https://www.conekta.com/) card token

## Installation

Add _conekta_tokenizer_ as a dependency in [your pubspec.yaml file](https://flutter.io/platform-plugins/).

```
conekta_tokenizer: ^1.0.0
```

### Android

Add Internet permission to Android project
```
<uses-permission android:name="android.permission.INTERNET"/>
```

Add to Android Manifest inside application tag
```
<uses-library android:name ="org.apache.http.legacy" android:required ="false"/>
```

### iOS  

If you are compiling with iOS 9, add the following lines to your application plist:
```
<key>NSAppTransportSecurity</key>
<dict>
<key>NSAllowsArbitraryLoads</key>
<true></true>
</dict>
```

## Usage

Instantiate the `ConektaTokenizer` class

	final conektaTokenizer = ConektaTokenizer();

Set your Conekta API Key

	conektaTokenizer.setApiKey("key_CUcWMZnt5zvqwePs2m432TQ");

When you already have your card information create an instance of `ConektaCard` and create the card token

	final conektaCard = ConektaCard(
		cardName: 'Alfonso Osorio',
		cardNumber: '4242424242424242',
		cvv: '847',
		expirationMonth: '12',
		expirationYear: '2040',
	);
	
	try {
		final String token = await conektaTokenizer.createCardToken(conektaCard);
	} on PlatformException catch (exception) {
		// Handle exception
	}

## Errors

The plugin can return the following errors

**ApiKeyNotProvided** This is because the Conekta API Key was not assigned

**InvalidCardArguments** This is because one or more card arguments are null or empty

> The library does not validate or verify that the data provided in the ConektaCard instance is correct, for example, the length of the cvv or the card number is valid.

In addition to the errors mentioned, the plugin also returns the errors that Conekta directly returns when trying to create the card token, for more information see https://developers.conekta.com/api#errors