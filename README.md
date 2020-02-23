# 

![Version](https://img.shields.io/badge/version-1.0-blue)
> It contains guides, libraries, cookbooks, code snippets to cover different aspects of an web application server. This is more a personal view of things that are important for a project but you can prioritize by your needs. The tools that I recommend are mostly open source/free. 
## Table of contents
* [Code Quality](#code-quality)
    * [Automatic checking](#auto-check)
    * [Manual checking](#manual-check)
 * [Security](#security)
    * [Auditing for OWASP Top 10](#owasp)
    * [SSL/TLS](#tls)
    * [Security Headers](#security-headers)
 * [Legal](#legal)
    * [Software Licences](#compl-lic)
    * [Data protection laws](#data-pr-laws)
 * [Defensive Programming](#def)
    * [Preconditions](#pre)
    * [Corner case errors](#cornercase)
 * [Test-Driven Development](#tdd)
    * [Training the TDD mindset](#tdd-mindset)
    * [Behavioral-Driven Development](#bdd)
    * [Testing priorities](#testing-prio)
    * ["The circle of purity"](#purity)
 * [Transactions](#tx)
    * [Local Transactions](#local-tx)
    * [Distributed Transactions](#dist-tx)
 * [Resiliency](#resiliency)       
 * [Fault Tolerance](#fault-tol) 
 * [Load Balancing](#load-balancing) 
 * [Transparent Deployment](#tr-depl) 
 * [Supervising](#supervising) 
 * [Logging](#log) 
 * [Monitoring](#monitor) 
 * [Metrics](#metrics) 
 * [High Availability](#high-avaibility) 
 * [Backup/Restore process](#backup)

 
## Code quality
> The term <em>'code quality'</em> is a bit vague in general, we can understand code quality as everything related to code consistency, readability, performance, test coverage, vulnerabilities...
### Automatic checking
#### Tools
 * SonarQube (Tip: Use a custom configuration that fits your project)
 * FindBugs
 * Checkstyle
#### Linters
 * SonarLint
### Manual checking
 > There are two books I personally encourage you to read them about '<em>clean code</em>'. There are also a ton of articles/videos on the internet related to this subject:
* 'Clean code' by Robert C. Martin :book:
    * [Cheat Sheet PDF](https://www.planetgeek.ch/wp-content/uploads/2014/11/Clean-Code-V2.4.pdf)  
    * [gist-based summary](https://gist.github.com/wojteklu/73c6914cc446146b8b533c0988cf8d29)
* 'Refactoring' by Martin Fowler, Kent Beck :book:
* [Patterns and Principles](https://java-design-patterns.com/) :globe_with_meridians:
* [CleanCoders: Elevate your skill with software training videos](https://cleancoders.com/) :tv:
## Security
### Auditing for [OWASP Top 10](https://owasp.org/www-project-top-ten/)
  * [OWASP Top 10 Common scenarios and preventions](https://www.owasp.org/images/0/0a/OWASP_Top_10_2017_GM_%28en%29.pdf)
### SSL/TLS 
 > SSL/TLS, the standard technology for keeping an internet connection secure and safeguarding any sensitive data that is being sent between two systems, preventing criminals from reading and modifying any information transferred, including potential personal details. The two systems can be a server and a client (for example, a shopping website and browser) or server to server (for example, an application with personal identifiable information or with payroll information)

 * [What it is?](https://www.acunetix.com/blog/articles/tls-security-what-is-tls-ssl-part-1/)
 * [Let's encrypt: Free TLS/SSL certificates](https://letsencrypt.org/)
 * [Some TLS/SSL vulnerabilities you should be aware](https://www.acunetix.com/blog/articles/tls-vulnerabilities-attacks-final-part/)
 * [Benefits of using HTTPS across your entire site](https://www.websecurity.digicert.com/security-topics/https-everywhere)
 
### Security Headers
 * `X-Frame-Options` - Sites can use this to avoid clickjacking attacks, by ensuring that their content is not embedded into other sites.
 * `X-Content-Type-Options` - Configuring your server to return the `X-Content-Type-Options` HTTP response header set to `nosniff` will instruct browsers that support MIME sniffing to use the server-provided `Content-Type` and not interpret the content as a different content type.
 * `Content-Security-Policy` - This helps guard against cross-site scripting attacks (XSS)
 * `X-XSS-Protection` - Stops pages from loading when they detect reflected cross-site scripting (XSS) attacks. Although these protections are largely unnecessary in modern browsers when sites implement a strong `Content-Security-Policy` that disables the use of inline JavaScript (`'unsafe-inline'`), they can still provide protections for users of older web browsers that don't yet support CSP 
 * `Strict-Transport-Security` - Lets a web site tell browsers that it should only be accessed using HTTPS, instead of using HTTP.
 * `Public-Key-Pins` - Associates a specific cryptographic public key with a certain web server to decrease the risk of MITM attacks with forged certificates

## Legal
### Software licences
> A software license is a legal instrument governing the use or redistribution of software
#### Licences types
 * **Public domain** - Anyone can modify and use the software without any restrictions
 * **Permissive** - They contain minimal requirements about how the software can be modified or redistributed. Popular with free and open source software
 * **LGPL** - If you simply compile or link an LGPL-licensed library with your own code, you can release your application under any license you want, even a proprietary license. But if you modify the library or copy parts of it into your code, you’ll have to release your application under similar terms as the LGPL.
 * **Copyleft** - These licenses allow you to modify the licensed code and distribute new works based on it, as long as you distribute any new works or adaptations under the same software license. Any derivative you create would also be limited to personal use only. “Derivatives” includes any new software you develop that contains the component. The catch here is that any end user of your software also has the right to modify the code. Therefore, you must make your own source code available. Exposing your source code may not be in your best interests.
 * **Proprietary** - All rights are reserved. It’s generally used for proprietary software where the work may not be modified or redistributed

#### Licence compliance utilities & tools
 * [Choose a licence by your needs](https://choosealicense.com/)
 * [Lookup for software licence permissions & restrictions](https://tldrlegal.com/)
 * [FOSSA - Continuous dependency tracking & license checks to keep your code compliant](https://fossa.com/)
 * [FOSSology - open source license compliance software system and toolkit](https://www.fossology.org/)

### Data protection laws
> Prohibits the disclosure or misuse of information about private individuals
 * [Data protection laws around the world](https://www.dlapiperdataprotection.com/)
 * [Data protection Impact Assessment](https://github.com/simonarnell/GDPRDPIAT/blob/master/Data%20Protection%20Impact%20Assessment.pdf)

## Defensive programming 
> Defensive programming ensures the continuing function of a piece of software under unforeseen circumstances. 

> Defend against the impossible, because the impossible will happen.  

> It aids the future maintainer of the code
### Preconditions
> A condition or predicate that must always be true just prior to the execution of some section of code.

 * Guava `Precondtions`:
 ```java
 public void accept(int value, Object myObj) {
  Preconditions.checkArgument(value >= 0, "negative value");
  Preconditions.checkNotNull(myObj);
  ...
}
 ``` 
 * Apache Commons `Validate`
  ```java
  public void accept(int value, Object myObj) {
   Validate.isTrue(value >= 0, "negative value");
   Validate.notNull(myObj);
   ...
 }
  ``` 

 * Others
    * [Spring Assertions](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/util/Assert.html)
    * [valid4j - design by contract](http://www.valid4j.org/)
    * [Bean Validation JSR-303](https://jcp.org/en/jsr/detail?id=303)
### Corner case errors
> Occurs outside of normal operating parameters, specifically when multiple environmental variables or conditions are simultaneously at extreme levels, even though each parameter is within the specified range for that parameter
 * [Java corner cases cheat sheet](https://ge0ffrey.github.io/ge0ffrey-presentations/cornerCaseCheatSheet/#/
)
 * [Common concurrency pitfalls](https://www.baeldung.com/java-common-concurrency-pitfalls)
