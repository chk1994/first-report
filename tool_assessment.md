# Tool Assessment

## Application Integration

Our project uses Representational State Transfer (REST) API for communication between the client and the server. Using REST for development allows for Separation of Concerns, where the client-side code will not concern itself with writing SQL statements or the logic for accessing the database. Rather, it will only largely concern itself with the View. Furthermore, by having Separation of Concerns: 
1. Development of user interface, the server and the data storage can be performed independently as they are loosely coupled to each other
1. Debugging and spotting security flaws in our project becomes easier

Our project uses [Spring framework](https://spring.io/) to create a secure and [RESTful web service](https://spring.io/guides/gs/serving-web-content/). Security is enforced through:
1. [Authentication for Web Application](https://spring.io/guides/gs/securing-web/)
1. [Roles & Privileges](https://www.baeldung.com/role-and-privilege-for-spring-security-registration)
1. [Method Security](https://www.baeldung.com/spring-security-method-security)

Spring only allows us to easily [connect and perform operations to a MySQL database](https://spring.io/guides/gs/accessing-data-mysql/).

Spring is also well-established and there are multiple useful guides for us to follow such as [developing an application using Spring from scratch](https://spring.io/guides/tutorials/bookmarks/).

Since Spring only works on Java platform, Java will be used for server side development.

## Anonymising Data

[Anonymising](http://kau.diva-portal.org/smash/get/diva2:1043735/FULLTEXT01.pdf) data makes it impossible to:
1. Single out an individual in the dataset. 
1. Link records concerning the same individual.
1. Infer the value of one attribute based on other values.

This allows for researchers to retrieve data for research purposes without violating privacy concerns.

There are 3 ways to ensure data anonymity:
1. [k-anonymity](https://en.wikipedia.org/wiki/K-anonymity), where at least k individuals in the dataset share the same set of attributes. This is implemented by:
    1. Suppression. For instance, all or some values of a particular column may be omitted through replacing them with "\*".
    1. Generalisation. For instance, the medical condition can be replaced with a more general term (e.g., “Cardiovascular disease” replaced with “Heart-related”).
    
    Example of pre-anonymised data:
    
    ![pre-anonymised data](https://github.com/IFS4205-2018-Sem1-Team1/first-report/raw/master/images/pre_anonymisation.png)
    
    After applying 2-anonymity to the data. Notice that this data has 2-anonymity with respect to the attributes "Age" and "Gender", but not for the attribute "Disease":
    
    ![post-anonymised data](https://github.com/IFS4205-2018-Sem1-Team1/first-report/raw/master/images/post_anonymisation.png)

1. [Adding noise to the data](https://link.springer.com/article/10.1186/s40537-017-0110-7). This can be implemented by swapping cells within columns.

1. Generating fake data, where the fake data must be a good representation of the actual data.

Since anonymising data is not the key focus of the project, we decided not to spend time to implement the algorithms if possible. Out of the 3 methods discussed above, only k-anonymity has an existing well-established [library](https://arx.deidentifier.org/overview/), complete with [examples](https://github.com/arx-deidentifier/arx/tree/master/src/example/org/deidentifier/arx/examples). Therefore, k-anonymity will be used to ensure data anonymity.

## Encryption

The purpose of [encryption](https://en.wikipedia.org/wiki/Encryption) is to ensure data transfer traffic is not susceptible to potential interceptors. Encryption will be used when data is transferred between the 3 different servers, namely front-end, back-end, and database.

Example of encryption:
![encryption-example](https://github.com/IFS4205-2018-Sem1-Team1/first-report/raw/master/images/public_key_encryption_keys.png)

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

Our project uses [GitHub](https://github.com/IFS4205-2018-Sem1-Team1) for source code control and issue management because most of the team are familiar and comfortable with using GitHub. This is not the case for the alternatives.

There are other alternatives such as:
1. Bitbucket. It allows free hosting of private repositories. However, the free version only allows for up to 5 users per repository. As our team has 6 members, we are not able to use the free version. Furthermore, there is no requirement to host our code on private repositories. 
Therefore, there's no compelling reason for us to use Bitbucket over GitHub.
1. GitLab. GitLab has inbuilt CI/CD, which means that we do not have to manually integrate external CI/CD tools to our repositories. This is a plus point, though, not a very big one since it's easy to manually integrate external CI/CD tools. 
However, GitLab is lacking some features compared to GitHub. For example, an issue can only be assigned to a single developer. There may be occasions when we need to assign multiple developers to resolve a certain issue, perhaps because that issue is hard. 
Therefore, there's no compelling reason for us to use GitLab over GitHub.

Reports will be written in .md (instead of .doc) to allow for version control of reports as well.

## DevOps Tools

Our project will use [Ansible](https://www.ansible.com/) to ensure that our remote servers are all set up with the same configuration.  [This doc](https://docs.ansible.com/ansible/2.5/user_guide/intro_getting_started.html) will help us with setting up. 

## Security Tools

To scan our web application for vulnerabilities like XSS, we will use [Metaspolit](https://www.metasploit.com/) and [Arachni](http://www.arachni-scanner.com/). 

To scan our PHP code for vulnerabilities and weaknesses related to security, [phpcs-security-audit](https://github.com/FloeDesignTechnologies/phpcs-security-audit) will be used. 

To find and fix known vulnerabilities in open-source dependencies, we would also use [Synk](https://github.com/Snyk/) that can be integrated easily with our Github repo

We can also consider using [BDD-Security](https://www.continuumsecurity.net/bdd-security/) to launch automated scans with specific scenarios/ claims we want to keep. 
