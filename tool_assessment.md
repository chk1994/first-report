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
    
    ![pre-anonymised data](https://github.com/IFS4205-2018-Sem1-Team1/first-report/raw/master/images/pre_anonymisation.png)
    
    After applying 2-anonymity to the data. Notice that this data has 2-anonymity with respect to the attributes "Age" and "Gender", but not for the attribute "Disease":
    
    ![post-anonymised data](https://github.com/IFS4205-2018-Sem1-Team1/first-report/raw/master/images/post_anonymisation.png)

1. [Adding noise to the data](https://link.springer.com/article/10.1186/s40537-017-0110-7). This can be implemented by swapping cells within columns.

1. Generating fake data. The fake data must be a good representation of the actual data.

Since anonymising data is not the key focus of the project, we decided not to spend implement the algorithms if possible. Out of the 3 methods, only k-anonymity has an existing well-established [library](https://arx.deidentifier.org/overview/), complete with [examples](https://github.com/arx-deidentifier/arx/tree/master/src/example/org/deidentifier/arx/examples). Therefore, we've decided to use k-anonymity.

## Secure Data Transfer
We intend to have a web application in which [authorization](https://en.wikipedia.org/wiki/Authorization) is handled by [Apache Shiro](https://shiro.apache.org/) and [authentication](https://en.wikipedia.org/wiki/Authentication) by [JSON Web Token (JWT)](https://jwt.io/).

Apache Shiro is a powerful and easy to use Java security framework that offers developers an intuitive yet comprehensive solution to:
1. Authentication
1. Authorization
1. Cryptography
1. Session Management

Although Apache Shiro already has a authorization functionality built into its library, we decide to employ the use of JWT for this purpose instead as JWT is much easier to implement as a Single Sign-On (SSO). In addition, it removes the need for cookies and session which is required in Apache Shiro's framework. Since JWT only provides authorization, we would still require Apache Shiro for authentication.

JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. A JWT is actually a string consisting of three parts: Header, Payload, and Signature. The JWT can encrypt the secret using the [Hash-based Message Authentication Code (HMAC)](https://en.wikipedia.org/wiki/HMAC) algorithm or sign it using the [Rivest–Shamir–Adleman (RSA)](https://en.wikipedia.org/wiki/RSA_(cryptosystem)) public and private key. The purpose of [encryption](https://en.wikipedia.org/wiki/Encryption) is to ensure data transfer traffic is not susceptible to potential interceptors. This JWT is then presented everytime the subject requests protected resources.

The following diagram shows how a JWT is obtained and used to access APIs or resources:

![jwt_example](https://github.com/IFS4205-2018-Sem1-Team1/first-report/raw/master/images/jwt_example.png)

A justification for the use of JWT is because it comes with a huge [library](https://jwt.io/#libraries) supported for many different programming languages.

When we use Apache Shiro to implement the login system, a JWT information is returned to the front-end, and it stores the token information in the request header when it interacts with the back-end server. We will then configure a custom interceptor to intercept all URL requests, retrieve the token information in the request header information, and verify the token information. If the token information generated during the login is correct, the user is logged in. Otherwise, we will reject the request and return a 401 error.

## Source Code Control & Issue Management

Our project uses [GitHub](https://github.com/IFS4205-2018-Sem1-Team1) for source code control and issue management for the following reasons:
1. It's a good tool for project management.
1. Most of the team are familiar and comfortable with using GitHub. This is not the case for the alternatives.

There are other alternatives such as:
1. Bitbucket. It allows free hosting of private repositories. However, the free version only allows for up to 5 users per repository. As our team has 6 members, we are not able to use the free version. Furthermore, there is no requirement for us to host our code on private repositories.
1. GitLab. GitLab has inbuilt CI/CD. This means that we do not have to manually integrate external CI/CD such as Travis to our repositories. This is a plus point, though, not a very big one since it's easy to perform manual integration of external CI/CD. 
Also, GitLab is lacking some features compared to GitHub such as having only a single assignee for issues. Since some issues may be quite hard to resolve, we may need to use GitHub's feature of having multiple assignees for issues. 
Therefore, there's no compelling reason for us to use GitLab over GitHub.

Reports will be written in .md (instead of .doc) to allow for version control of reports as well.

## DevOps Tools

Our project will use [Ansible](https://www.ansible.com/) to ensure that our remote servers are all set up with the same configuration.  [This doc](https://docs.ansible.com/ansible/2.5/user_guide/intro_getting_started.html) will help us with setting up. 

## Security Tools

To scan our web application for vulnerabilities like XSS, we will use [Metaspolit](https://www.metasploit.com/) and [Arachni](http://www.arachni-scanner.com/). 

To scan our PHP code for vulnerabilities and weaknesses related to security, [phpcs-security-audit](https://github.com/FloeDesignTechnologies/phpcs-security-audit) will be used. 

To find and fix known vulnerabilities in open-source dependencies, we would also use [Synk](https://github.com/Snyk/) that can be integrated easily with our Github repo

We can also consider using [BDD-Security](https://www.continuumsecurity.net/bdd-security/) to launch automated scans with specific scenarios/ claims we want to keep. 
