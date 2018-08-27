# Tool Assessment

## Anonymising Data

The purpose of [anonymising](http://kau.diva-portal.org/smash/get/diva2:1043735/FULLTEXT01.pdf) data is to make it impossible to:
1. Single out an individual in the dataset. 
1. Link records concerning the same individual.
1. Infer the value of one attribute based on other values.

This allows for researchers to retrieve data for research purposes without violating privacy concerns.

There are 3 ways to ensure anonymity of data:
1. [k-anonymity](https://en.wikipedia.org/wiki/K-anonymity). This is implemented by:
    1. Suppression. For instance, all or some values of a particular column may be omitted through replacing it with a "\*".
    1. Generalisation. For instance, the medical condition can be replaced by a more general term (e.g., “Cardiovascular disease” replaced by “Heart-related”).
    
    An example of pre-anonymised data:
    
    ![pre-anonymised data](/images/pre_anonymisation.png)
    
    After applying 2-anonymity to the data. Notice that this data has 2-anonymity with respect to the attributes "Age" and "Gender", but not for the attribute "Disease":
    
    ![post-anonymised data](/images/post_anonymisation.png)

1. [Adding noise to the data](https://link.springer.com/article/10.1186/s40537-017-0110-7). This can be implemented by swapping cells within columns.

1. Generating fake data. The fake data must be a good representation of the actual data.

Since anonymising data is not the key focus of the project, we decided not to spend implement the algorithms if possible. Out of the 3 methods, only k-anonymity has an existing well-established [library](https://arx.deidentifier.org/overview/), complete with [examples](https://github.com/arx-deidentifier/arx/tree/master/src/example/org/deidentifier/arx/examples). Therefore, we've decided to use k-anonymity.

## Encryption

The purpose of [encryption](https://en.wikipedia.org/wiki/Encryption) is to ensure data transfer traffic is not susceptible to potential interceptors. Encryption will be used when data is transferred between the 3 different servers, namely front-end, back-end, and database.

Example of encryption:
![encryption-example](/images/public_key_encryption_keys.png)

There is a useful cryptographic class for use in [Java Platform SE 10](https://docs.oracle.com/javase/10/docs/api/javax/crypto/Cipher.html):
1. Symmetric Key Encryption (AES)
1. Asymmetric Key Encrytion (RSA)

Advanced Encryption Standard (AES) is a symmetric algorithm (private-key cryptography). This involves a single key which is a shared secret between the sender and recipient. The same key is being used for both encryption and decryption. Public-key cryptography (PKI), a asymmetric algorithm, involves two related keys for each recipient involved - a private key which is a secret known only by the recipient, and a related public key which is known by all senders. The sender encrypts the message using the recipient's public key. That message can only be decrypted by a recipient with a private key matching the public key. We will be using RSA for our asymmetric algorithm.

For simplicity and efficient encryption, we can employ the use of AES with a single secret key for encryption and decryption. The secret key used has to be stored in a safe location to prevent any potential compromise. We propose to lock it in a password protected .config file that outsiders are unable to access.

Possible library alternatives:
1. [PHP](http://php.net/manual/en/refs.crypto.php)
1. [Python](https://docs.python.org/3/library/crypto.html)
1. [Perl](https://perldoc.perl.org/functions/crypt.html)

AES [example](https://aesencryption.net/).

## Source Code Control & Issue Management

Our project uses [GitHub](https://github.com/IFS4205-2018-Sem1-Team1) for source code control and issue management. Reports will be written in .md (instead of .doc) to allow for version control of reports as well.

## DevOps Tools

Our project will use [Ansible](https://www.ansible.com/) to ensure that our remote servers are all set up with the same configuration.  [This doc](https://docs.ansible.com/ansible/2.5/user_guide/intro_getting_started.html) will help us with setting up. 

## Security Tools

To scan our web application for vulnerabilities like XSS, we will use [Metaspolit](https://www.metasploit.com/) and [Arachni](http://www.arachni-scanner.com/). 

To scan our PHP code for vulnerabilities and weaknesses related to security, [phpcs-security-audit](https://github.com/FloeDesignTechnologies/phpcs-security-audit) will be used. 

To find and fix known vulnerabilities in open-source dependencies, we would also use [Synk](https://github.com/Snyk/) that can be integrated easily with our Github repo

We can also consider using [BDD-Security](https://www.continuumsecurity.net/bdd-security/) to launch automated scans with specific scenarios/ claims we want to keep. 
