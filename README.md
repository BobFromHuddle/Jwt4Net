Jwt4Net is a C# library for issuing and consuming Json Web Tokens.

It offers strongly typed token values, and a simple model for issuance and consumption.
Validation of tokens is extensible by creating new implementations of ITokenValidationRule, and tokens can contain arbitrary claims.

```C#
var issuer = JwtContainer.CreateIssuer();
issuer.Set(MyClaims.Age, 21);
issuer.Set(MyClaims.Name, "Hubert von Peeblefruit");

string tokenString = issuer.Sign();

JsonWebToken token;
var consumer = JwtContainer.CreateConsumer();
if(false == consumer.TryConsume(tokenString))
{
  throw new WonkyTokenException(consumer.FailureReason);
}

int age = token.Claims.Get(MyClaims.Age).Value;
string name = token.Claims.Get(MyClaims.Name).Value;
```


Jwt4Net is currently at beta stage 0.8:

*  Elliptic curve signing is fully supported
*  RSA signing is enabled in principle, but the management is poor and bugs are expected.
*  HMAC signing works.
*  KeyTool now replaces all the one-trick applications for managing keys.
*  Public keys are distributed in PEM format and private keys are exportable in PFX.


Still to do:

0.9

* Add full RSA key Support
* Allow HMAC signing to use the machine-key
* Rename ES512 to ES521 (doh)

1.0

* Refactor keytool to reduce the complexity of the code
* Fix up documentation, increase test coverage from its terrifying nadir

1.1 

* Clean up the abysmal fluent configuration
* Tidy up the xml config - do we need to specify the algorithm?

2.0

* Support CngProviders and user/machine keys properly
* Split JWT from JWS.
* Implement JWS encryption
* Implement JSON-encoded public key certificates