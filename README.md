# 

![Version](https://img.shields.io/badge/version-1.0-blue)

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
 * [Testing](#tdd)
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

## Testing

> Unit testing is a level of software testing where individual units/ components of a software are tested.

### Test-Driven Development (TDD)

True Test-Driven Development is very simple, it is "**RED, GREEN, REFACTOR**"
 - We write a test, run it and see it fail (**RED**).
 - We write the minimum code to make it pass, run it and see it pass (**GREEN**).
 - We refactor the code, and the test, to make them as clean, expressive, elegant and simple as we can imagine (**REFACTOR**).
 
For most of developers it can be a uncomfortable process but it can be trained using [Katas](https://en.wikipedia.org/wiki/Karate_kata):
* [TDD Katas](https://github.com/wix/tdd-katas)

### Behavioral-Driven Development (BDD) structure

> The goal of BDD is a business readable and domain-specific language that allows you to describe a system’s behavior without explaining how that behavior is implemented.

It helps also to structure your unit tests like this:

```
“As a [role] I want [feature] so that [benefit]”. Acceptance criteria should be written in terms of scenarios and implemented as classes:
Given [initial context],
when [event occurs],
then [ensure some outcomes].
```

For example, [Spock Framework](http://spockframework.org/) is using a BDD structure:
```
def "events are published to all subscribers"() {
  given:
  def subscriber1 = Mock(Subscriber)
  def subscriber2 = Mock(Subscriber)
  def publisher = new Publisher()
  publisher.add(subscriber1)
  publisher.add(subscriber2)

  when:
  publisher.fire("event")

  then:
  1 * subscriber1.receive("event")
  1 * subscriber2.receive("event")
}
```

### Testing goals

1. Tests should be **sensitive** and should fail for any bug
2. Tests should be **maintainable**:
   * Expressive
   * Isolated
   * Robust
   * Low overlap
   * Fast
   * Small
3. Tests should bring real value to your project. Do not aim for high coverage as a number. Aim to cover weak spots of your code. Tests should be **ruthless** and should have **no mercy** to your code. 

### Testing priorities

> What should you test first?

1. Code that is hard to understand
2. Code that takes a long time to reproduce using the UI/Dev/Manual testing
3. Bugs (before fixing it)
4. `for`/`if`/`while`
5. Thrown exception
6. A method that just call other methods
7. Trivial code like `setters` or `getters`
8. Legacy code with no bugs or changes

### Risk-Driven Testing (from [Google Testing Blog](https://testing.googleblog.com/))

We are all conditioned to write tests as we code: unit, functional, UI. We are professionals, after all. Many of us like how small tests let us work quickly, and how larger tests inspire safety and closure. Or we may just anticipate flak during review. We are so used to these tests that ofter we no longer question why we write them. This can be wasteful and dangerous. 

Tests are a means to an end. To reduce the key risks of a project, and to get the biggest bang for the buck. This bang may not always come from the tests that standard practice has you write, or not even from tests at all.

Two examples:

###### Example #1
> "We built a new debugging aid. We wrote unit, integration, and UI tests. We were ready to launch."

Outstanding practice. **Missing the mark**

Our key risks were that we'd corrupt out data or bring down our servers for the sake of a debugging aid. None of the tests addressed this, but they gave a false sense of safety and "being done".
**We stopped the launch**

###### Example #2
> "We wanted to turn down a feature, so we needed to alert affected users. Again we had unit and integration tests, and even one expensive end-to-end test."

Standard practice. **Wasted effort**

The alert was so critical it actually needed end-to-end coverage for all scenarios. But it would be live for only three releases. The cheapest effective test? Manual testing before each release. 

**A better approach: Risks First**

For every project or feature, *think* about testing. Brainstorm your key risks and your best options to reduce them. Do this at the start so you don't waste effort and can adapt your design. Write them down as a QA design so you can point to it in reviews and discussions. 
To be sure, standard practice remains a good idea in most cases. Small tests are cheap and speed up coding and maintenance, and larger tests safeguard core use-cases and integration. 

Just remember: Your tests are a means. **The bang is what counts**. It's your job to **maximize it**.

### Change-Detector Tests Considered Harmful (from [Google Testing Blog](https://testing.googleblog.com/))

You have just finished refactoring some code without modifying its behavior. Then you run the tests before committing and... a bunch of unit tests are failing. While fixing the tests, you get a sense that you are wasting time by mechanically applying the same transformation to many tests. Maybe you introduced a parameter in a method, and now must update 100 callers of that method in tests to pass an empty string.

What does it look like to write tests mechanically? Here is an absurt but obvious way:

```
// Production code
def abs(i: Int)
   return (i < 0) ? i * -1 : i
   
// Test code
for (line: String in File(prod_source).read_lines())
   switch (line.number)
      1: assert line.content equals "def abs(i: Int)"
      2: assert line.content equals "  return (i < 0) ? i * -1 : i"
```

That test is clearly not useful: it contains an exact copy of the code under test and acts like a checksum. A correct or incorrect program is equally likely to pass a test that is a derivative of the code under test.
No one is really writing tests like that, but how different is it from this next example?

```
// Production code
def process(w: Work)
   firstPart.process(w)
   secondPart.process(w)

// Test code

// given
part1 = mock(FirstPart)
part2 = mock(SecondPart)
w = Work()

// when
Processor(part1, part2).process(w)

// then
verify_in_order
   was_called part1.process(w)
   was_called part2.process(w)
```

It is tempting to write a test like this because it requires little thought and will run quickly. This is a change-detector test—it is a transformation of the same information in the code under test—and it breaks in response to any change to the production code, without verifying correct behavior of either the original or modified production code.

Change detectors provide negative value, since the tests do not catch any defects, and the added maintenance cost slows down development. These tests should be re-written or deleted. 
