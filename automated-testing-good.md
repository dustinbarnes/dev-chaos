---
description: >-
  Let's make a bold claim: automated tests are not for software validation or
  software verification.
---

# Automated Testing Good



{% hint style="info" %}
This is a repost of a blog article I wrote a while back for a site that no longer exists. It was originally published Feb 12, 2014. 

Modern \(Jan 29, 2019\) Take: Is this really even a debate anymore? I feel like the whole world has come around to the value of automated testing. It's so fundamental to the modern development workflow that any company not having tests is going to lose market traction to competitors who can meet the market more quickly.
{% endhint %}

## History <a id="history"></a>

Modern developers have been exposed to all sorts of automated testing concepts: Test-driven development, unit testing, integration testing, behavior-driven development, functional testing.

Despite this, some people and organizations have a strong aversion to automated tests. Their objections stem from the near-truths \("Our system is too complex to test"\), to the probably-false \("Testing doesn't provide any value"\) to the completely ignorant \("I don't know what a unit test is"\). In this article, we will make the case that automated testing provides business value at all tiers, and no matter how much you do, you're probably not doing enough.

## Redefining Terms <a id="redefiningterms"></a>

Forget the battles between emacs and vim and the wars of Microsoft and Linux. The real battle line of modern developers is the definition and distinction between unit tests and integration tests. Never has such effort been put into drawing ever-finer boundary lines between these layers of testing. In the end this distinction is ultimately meaningless.

Historically, unit tests are supposed to depend on nothing except the class or method under test. Developers mock or stub all external actors, and then test just the code you want to test. Integration tests referred to the testing of the application where some of the external systems are available and working. A classic example of this in the Java world is testing your JDBC connection strings. It's great to unit test them, but until you try to connect it to a live database, you don't actually know that it works for sure.

Instead of giving you our definition of these terms, we're going to focus on a different set of terms. Commit-, functional-, and acceptance-level tests.

### Commit Level Tests <a id="commitleveltests"></a>

Commit level tests happen, not surprisingly, when you commit the code. They are the first line of defense against breaking changes. These tests can be unit or integration, but the key feature of these tests is that they finish quickly. The entire commit level test suite should run in under 5 minutes. This keeps the feedback loop tight, and allows the continuous delivery pipeline to fail as quickly as possible.

### Functional Level Tests <a id="functionalleveltests"></a>

Functional level tests happen after the commit level tests happen. They are the gatekeeper between an artifact and promotion to the next environment. The tests here can take as long as needed to verify the software, but obviously, faster is better.

### Acceptance Level Tests <a id="acceptanceleveltests"></a>

These tests happen after the software has been deployed into an environment. They operate on the application to verify that everything is working as expected. Smoke tests are an example of acceptance-level tests.

## Validation and Verification <a id="validationandverification"></a>

These two terms are used interchangeably, but they are drastically different in the formal world of tests and proofs. Validation checks that the software meets the high-level requirements from a user's standpoint. It is validating that the requirements were correct in the first place. Verification means that the application was developed to the requirements appropriately. In short, validation is "building the right thing," and verification is "building the thing right."

Critics of automated tests often claim that it's impossible to prove the software is working correctly, so it's a waste of time. While they're correct in the first part, they're very wrong on the second part. No software, outside from a group of people whose work is largely research-oriented, is provably correct. Microsoft Windows isn't provably correct. Neither is Linux. Even Java isn't provably correct. Additionally, any formal proof of software correctness is only as good as the proofs themselves, and is dependent upon a formalized proof of the hardware correctness as well. Also, manual testing can't prove the software is correct. The inability to prove the correctness of software is, in our current world, a truism. It's also irrelevant.

## The Value Proposition <a id="thevalueproposition"></a>

Given that we understand automated tests can never prove software correct, why do we still do them? Let's make a bold claim: automated tests are not for software validation or software verification.

A lot of developers who practice TDD follow the red-green approach. They write tests, run them, and see the red lights. Then they build software, re-run the tests, and get a green light. That means the code you wrote works, right? Nope.

What you have done is codify a behavior. Given a certain set of inputs and the software as it was written, you have a certain set of outputs. You have a small chunk of _behavior_ validation.

Why do we make changes to software? It's usually to change the behavior of the software. Adding or removing a feature is changing the behavior. Fixing a bug is, in fact, changing the behavior. It was incorrect behavior, and that's why you write a new test to make sure the behavior never reverts accidentally.

In the process of changing the behavior of a system, you might have to make large changes to the software architecture. Given the potential scope of changes, how can you be reasonably sure that the _behavior of the system hasn't changed_?

If you eschewed automated testing because it can't prove anything, you have no idea that the behavior of the system hasn't changed. In order to get the most confidence, you need to run a full regression on the entire application. This is expensive, prone to human error, and has a high level of risk.

If you embrace automated testing, you have a set of tests that validate the stability of behavior in your system and the ability to make large changes to your code base. This guarantees that the software behavior did not change. This is where the real value in automated testing lies.

## The Extended Value Proposition <a id="theextendedvalueproposition"></a>

Automated tests don't check that your code is doing the right thing. They document your code in such a way that anybody can check that it continues to behave in the same way after some changes are made in the code. 

This has some very interesting implications. The primary one is that **your tests specify exactly what your business does**. If you don't validate the consistency of behavior, that means the behavior is not important to your business.

This reason is why BDD, or Behavior Driven Development, has emerged as a technique to capture system behaviors at a very high level, often in text format. A developer or SDET then works with the business people to write some code to execute these behavior requirements automatically, and with every code change. With enough of these behavior scenarios, we end up with a living specification of your business. You could execute a re-platforming \(moving from PHP to Java, for example\) using these high-level behavior tests as a guide. Think about that for a minute. You could rebuild your software, and therefore your business, from these behavior specifications.

A bunch of green lights on tests doesn't mean that your software is perfect. It means that your business is doing what you think it should be doing.

This behavior specification, then, is \(arguably\) more valuable than the software itself. It becomes a living document that formally describes your business, and lets you know when that behavior changes unexpectedly. That's powerful. It's also very, very valuable.  


