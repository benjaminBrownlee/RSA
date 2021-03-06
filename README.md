# RSA.js
**RSA.js** is a javascript RSA algorithim encryption tool, complete with key generation and functions to encrypt, decrypt, encode, and decode strings.
## Installation
This library is built primarily for browser applications. Simply download it [here](https://raw.githubusercontent.com/benjaminBrownlee/RSA/master/RSA.min.js) or just hotlink to it:
      
	<script src="https://raw.githubusercontent.com/benjaminBrownlee/RSA/master/RSA.min.js"></script>
      
Also, RSA.js relies on bigInt.js to generate, compute, and manage massive values for encryption. Keys, encoded strings, and encrypted strings will be represented as Big Integer objects.  Download bigInt.js [here](http://peterolson.github.com/BigInteger.js/BigInteger.min.js) or use the hotlink below:

	<script src="http://peterolson.github.com/BigInteger.js/BigInteger.min.js"></script>
## Usage
#### `RSA.generate(keysize)`
You can generate an encryption key of a given keysize (in bits), using `RSA.generate()`. This function will return an object with "n", "e", and "d" properties, standing for the publc key, public exponet, and private key respectively, where the public key is the number of bits given in the argument.

#### `RSA.encode(string)`
Convert a string of alphanumerical characters to standard utf-8 decimal encoding.  Only numbers can be encrypted, so an encoding is necessary to encrypt any non-numerical data.

#### `RSA.encrypt(data, public_key, public_exponet)`
Encrypt numerical data using public parts of a generated or transmitted key.  These will be the "n" and "e" properties in the object returned by the `RSA.generate()` function.  Function will throw an error if any of the arguments are not Big Integer objects.

#### `RSA.decrypt(cipher_text, private_key, public_key)`
Using the private part of the encryption key (which should not be transfered via network), decrypt a cipher-text string of numerals. Will return an encoded string or simply a number, depending on intent of data transmission

#### `RSA.decode(number)`
Revert data back to string form if it was originally encoded in utf-8 code.

## Worked Example
Here is a worked example of how to use RSA.js to encrypt and decrypt a JS string:

	var keys = RSA.generate(250);
	var message = RSA.encode("Successful RSA process!");
	var encrypted_message = RSA.encrypt(message, keys.n, keys.e);
	var decrypted_message = RSA.decrypt(encrypted_message, keys.d, keys.n);
	var decoded_message = RSA.decode(decrypted_message);
	message === decoded_message ? alert("Success!") : alert("Error!");
