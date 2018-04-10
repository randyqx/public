# Using a Yubikey in Static Mode Plus Passphrases

For authentication, there is an aphorism that a credential should
consist of something you have, e.g. a token card, and something you
remember, e.g. a passphrase.  This is sarcastically known as something
you have lost and something you have forgotten.

On the theme of something you've lost and something you have forgotten,
I use the following hack for basic MacOS login credentials, gpg, ssh,
etc.

## Something I Have Lost:

I have a [Yubukey Neo](https://www.yubico.com/), which has a long ugly
programmitically generated passphase I could never remember or type.  It
is in what Yubikey calls static pasword mode, i.e. punch the Yubikey and
it spits it out, slowly and without a terminating end of line (Yubikey
options when configuring).  Yes, I carry a spare key.

## Something I Have Forgotten:

Then, for each service, I have memorized a per-service simpler string,
which I type in and then finally hit return on the keyboard.  These
strings are the flavor of the first letter of words from a song or
literature; so I have a chance of getting them correctly.

The two concatenated strings, Yubikey and typed, form a per-service
passphrase.

Once I can get into my laptop and gpg decrypt my file of a thousand
keys, I'm good to go.

---

2017.08.26
