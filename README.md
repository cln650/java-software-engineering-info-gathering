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
 * [Defensive Programming Techniques](#def)
    * [Preconditions](#pre)
    * [Post-conditions](#post)   
    * [Mitigate corner case errors](#cornercase)
 * [Test-Driven Development](#tdd)
    * [Training the TDD mindset](#tdd-mindset)
    * [Behavioral-Driven Development](#bdd)
    * ["The circle of purity"](#purity)
 * [Legal](#legal)
    * [Compliant Licences](#compl-lic)
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
 * [Transactions](#tx)
    * [Local Transactions](#local-tx)
    * [Distributed Transactions](#dist-tx)
 
## Code quality
> The term <em>'code quality'</em> is a bit vague in general, we can understand code quality as everything related to code consistency, readability, performance, test coverage, vulnerabilities...
### Automatic checking
#### Tools
 * SonarQube (Project level configuration)
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
* [A paid video course related to clean code](https://cleancoders.com/) :tv:
## Security
### Auditing for [OWASP Top 10](https://owasp.org/www-project-top-ten/)
