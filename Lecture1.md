Note: These notes are based on my understanding of the lecture and may not be complete and accurate.
Lecture1: Introduction

# What is security? 
	Goal vs. Adversary

Security involves 3 concepts:
	Policy: This is the security goal defined
	Threat model: Assumptions made (of the adversary)
	Mechanism: Software/Hardware/System

Security can be compromised if there are weaknesses in any of the above 3 mentioned concepts.

Policy
	It is important to have a clear and accurate security policy defined.
For example, the security policy of an email login system defines that the way
to access the email account is by entering the password. In the circumstances
that the user forgot the password, the system allows him to reset password by
answering some security questions. So, the policy of the email login system
has now changed. Anyone who knows the password or knows the answers to the
security questions can login to the email account.

Threat model
	These are the assumptions made by the system/software developers about
the adversary. For example, the adversary does not have access to your phone
or laptop.

Example1: Assuming the adversary is only looking at ways to find
vulnerabilities in your code
In an interesting case, the adversary was was able to access the physical
server which had the OS code and introduced backdoor in the code

Example2: Assuming that a certificate can be trusted

Mechanism
	This is the mechanism that implements the security policy.

Example1: Wired Editor
The gmail account of the editor of Wired magazine was hacked a few years ago
and this is how the hackers did it. They requested a password reset for the
editor's Gmail account. Gmail then informed the requestor that it sent the
password reset link to the recovery email address, which in this case was the
editor's @me.com (Apple) email address. Gmail does not display the entire
recovery email address, but part of it, but this was sufficient for the
hackers to guess the recovery email address. They hacked his Apple email
address.

Hacking Apple email address
The hackers next requested password reset of the @me.com email address. For
the reset request to be accepted, Apple requires the email owner's billing
address and the last 4 digits of his registered credit card number. The
hackers easily obtained his billing address. To obtain his credit card number,
they hacked his Amazon account.
	
Hacking Amazon account
The hackers called the Amazon tech support and asked to add a new credit card
number to the editor's Amazon account. After being provided the correct email
address and the billing address, Amazon added the new credit card number. The
hackers called back Amazon and asked for a password reset. Amazon asked for
the details of one of the credit cards on the account. The hackers happily
provided the credit card they had just added to the account and thus, got
access to the editor's Amazon account. Now this account had the details of all
the credit cards the editor had added. Amazon displays only the last 4 digits
of the cards for security purposes. But these last 4 digits was all the
hackers needed to reset the Apple email address and then the Gmail email
account. 

Example2: How do certificates and languages differ in reading domain names in
certificates?
Most certificates determine the end of a domain by counting the number of
characters in the URL. For example, if the URL is www.amazon.com, then the
number of characters in it 14, but C reads end of string only when it
encounters \0. So if there is a domain called www.amazon.com\0xfoo.com, which
is a valid domain according to the CA, but C is going to read this as
www.amazon.com because it encounters \0.

Example3: Citi example
In of Citibank's websites (this might have been fixed now), you can view your account information by entering
your login credentials. Once you successfully login, you can see the URL
something as www.citi.com/id=1234. What hackers discovered was that if you
changed 1234 to another id, Citi redirected to another account without asking
you to login as the owner of the other id.

Example4: Find my iPhone example
Apple's cloud has different app interfaces. Even if one of them is weak, that
compromises the cloud. What hackers discovered that the Find my iPhone app
gives you unlimited attempts at trying the password, instead of giving you a
timeout after certain tries.
