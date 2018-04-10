# Hygiene Suggestions, Mac Oriented

This is a set of bullets.  Each of these could have a paragraph or a
page; but only bullets were commissioned :)

If this all seems too paranoid, perhaps you should look at [Paranoia
101](https://archive.psg.com/170605.Paranoia-101.pdf).

One always begins by thinking about what assets one is protecting and
what the threats are to those assets.

There will be (and probably have been) security incidents.  Whether you
detect them depends on how well you instrument.  How you handle them
depends on how well you prepare; see final item on this page.

## Assets

After people, sources, financial, customer, ... data are your principal
assets.  Hardware is easily replaced.

Data are vulnerable both when in flight and when at rest.  Techniques
for dealing with the two differ.

## Threats

Passwords are very vulnerable; especially to repositories such as
GitHub.  Employees lose passwords by 
* Spear fishing, whaling, ...  Do not trust email period
* Password re-use from Ashley Madison or whatever
* Ex-employees

Laptops are vulnerable, especially with source or credentials on them.
* They are accidentally lost
* They are stolen
* Note the 'evil maid attack', [ThunderStrike for
  example](https://trmm.net/Thunderstrike) (I do not leave my laptop in
  the hotel room)

## Stay Current

Keep Laptop, iFoos, servers, fully updated and patched.  But be careful
with pop-ups offering to update software; they can be used as an attack
vector.

As the user base scales, centralization of patch management, pushing of
patches, and tracking which laptops have, and have not, been patched
becomes important.  Apple supplies tools for centralized management.
Try to make it as un-annoying to the users as reasonably possible.

## Passwords

Use strong and unique passwords.

Use a password manager such as [1Password](https://1password.com/) to
generate and store passwords.

Consider [YubiKey](https://www.yubico.com/) or some equivalent.  I use
it in combination with remembered phrases, [Something You Have and
Something You
Know](https://github.com/randyqx/public/blob/master/yubikey-static.md)

Again, be very aware of fishing and other credential exposure.

## Backup, Backup, Backup

Time Machine is strongly recommended.  A USB hard drive is simple and
inexpensive and will save your life.  When you initialize it, remember
to create it as encrypted and stash the passphrase somewhere safe.

You may alwo want to keep a distant backup far off site.  A lot of folk
lost everything in the California wildfires.

Use [Arq](https://www.arqbackup.com/) in encrypted mode to off-site
servers, AWS, or Google.  I prefer Google, as they have a better
reputation for protecting customers' data.

## Full Disk Encryption

Use [Full Disk Encryption](https://support.apple.com/en-us/HT204837)
(for Windows it is BitLocker).  You will not see a performance
difference.  Be sure to save the encryption backup keys; perhaps a
company security officer.

If you are an iCloud user, letting Apple remember your FDE backup key
for you is not unreasonable.  Apple does try to be good about your
security if a court order is not in your threat model.

## Screen Lock

Have your laptop lock quickly when not in use.

## Laptop Firewall

Turn on MacOSX's firewall in SystemPrefs/Security/Firewall.  This blocks
unwanted incoming traffic.

## Block Outgoing Leakage

Control and Block outgoing traffic by running [Little
Snitch](https://www.obdev.at/products/littlesnitch/).  It can be
annoying at first, as you decide if you want to allow port 42 to
foo.com; but it remembers well.

Its smaller sibling, [Micro
Snitch](https://www.obdev.at/products/microsnitch/), is useful for
alerting you when your microphone or camera are being used by anything.

## Encrypt

Encrypt as much as you can, both in flight and at rest.  There are many
and varied tools.

## Key Authentication

Use key authenticated application level crypto, not just transport, i.e.
Use RSA >= 2048 bits or ed25519.

Do not trust a VPN; for many things, you do not really know if it is on.
And it is only encrypting data in flight, not at rest.

Use keyed ssh as much as you can.

## Credential Scaling

As you get more employees, and employees come and go, you will need some
sort of credential management.  When an employee leaves, you can not go
GitHub, GMail, 19 devices, 42 servers, ... and remove their credentials.

As employees and services really scale, the cross-product becomes a
challenge to manage.  At that point, tools such as Kerberos and TLS
GSSAPI are worth evaluating.

## Prevent Malicious Boot

Make it so someone can not boot your Mac from their (USB or other)
drive, see [these
instructions](https://github.com/drduh/macOS-Security-and-Privacy-Guide#firmware)

## Protect Your Source

If your source is copied or stolen, they have your principal asset.
An attacker can copy it or they can use it to find vulnerabilities.

Do not use GitHub; one password slip by any single employee and you're
toast.

If you are only using GitHub as a git repository; a simple UNIX/Linux
server with an encrypted drive will do the job.

Guess how Juniper lost massive credibility when an attacker got to their
repository and inserted two backdoors.

If you want attribution in case of backdoors and other malicious
additions, consider [GPG signed
commits](https://github.com/randyqx/public/blob/master/signed-commits.md).

## Secure Mail

Use secure mail transports, i.e. imaps and smtps.

## iFoo

[Protect your iPhone](https://blog.filippo.io/securing-a-travel-iphone/)

Use [Firefox Focus](https://www.mozilla.org/en-US/firefox/focus/) as
your browser on phones and tablets.

Block browser tracking using Privacy Badger and Ublock Origin.

Block JavaScript, as much as you can, using a extension such as
NoScript.

It is OK to let your browser remember passwords; but prefer 1Password.

## Have a Plan

Your organization should have a plan for how to deal with security
incidents of various types.  There should be known roles for different
tasks (systems, laptops, physical, ...).  There should be escalation and
notification procedures,

---

2018.04.10
