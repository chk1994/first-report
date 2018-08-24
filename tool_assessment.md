# Tool Assessment

## Anonymising Data

The purpose of [anonymising](http://kau.diva-portal.org/smash/get/diva2:1043735/FULLTEXT01.pdf) data is to make it impossible to:
1. Single out an individual in the dataset. 
1. Link records concerning the same individual.
1. Infer the value of one attribute based on other values.

There are 2 ways to ensure anonymity of data:
1. [k-anonymity](https://en.wikipedia.org/wiki/K-anonymity). This is implemented by:
    1. Suppression. For instance, all or some values of a particular column may be omitted through replacing it with a "\*".
    1. Generalisation. For instance, the medical condition can be replaced by a more general term (e.g., “Cardiovascular disease” replaced by “Heart-related”).
    
    An example of pre-anonymised data:
    
    ![pre-anonymised data](/images/pre_anonymisation.png)
    
    After applying 2-anonymity to the data. Notice that this data has 2-anonymity with respect to the attributes "Age" and "Gender", but not for the attribute "Disease":
    
    ![post-anonymised data](/images/post_anonymisation.png)

1. [Adding noise to the data](https://link.springer.com/article/10.1186/s40537-017-0110-7). This is implemented by swapping cells within columns and replacing groups of k records with k copies of a single representative.

There's an existing well-established [library](https://arx.deidentifier.org/overview/) available to perform k-anonymity, complete with [examples](https://github.com/arx-deidentifier/arx/tree/master/src/example/org/deidentifier/arx/examples).

## Encryption

The purpose of [encryption](https://en.wikipedia.org/wiki/Encryption) is to ensure data transfer traffic is not susceptible to potential interceptors. Encryption will be used when data is transferred between the 3 different servers, namely front-end, back-end, and database.

Example of encryption:
![encryption-example](/images/public_key_encryption_keys.png)

There is a useful cryptographic class for use in [Java Platform SE 10](https://docs.oracle.com/javase/10/docs/api/javax/crypto/Cipher.html):
1. Symmetric Key Encryption (AES)
1. Assymetric Key Encrytion (PKI)

Advanced Encryption Standard (AES) is a symmetric algorithm (private-key cryptography). This involves a single key which is a shared secret between the sender and recipient. The same key is being used for both encryption and decryption. Public-key cryptography (PKI), a asymmetric algorithm, involves two related keys for each recipient involved - a private key which is a secret known only by the recipient, and a related public key which is known by all senders. The sender encrypts the message using the recipient's public key. That message can only be decrypted by a recipient with a private key matching the public key.

For simplicity and efficient encryption, we can employ the use of AES with a single secret key for encryption and decryption. The secret key used has to be stored in a safe location to prevent any potential compromise. We propose to lock it in a password protected .config file that outsiders are unable to access.

Possible library alternatives:
1. [PHP](http://php.net/manual/en/refs.crypto.php)
1. [Python](https://docs.python.org/3/library/crypto.html)
1. [Perl](https://perldoc.perl.org/functions/crypt.html)

AES [example](https://aesencryption.net/).
