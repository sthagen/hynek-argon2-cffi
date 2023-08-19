# What is Argon2?

:::{note}
**TL;DR**: Use {class}`argon2.PasswordHasher` with its default parameters to securely hash your passwords.

You do **not** need to read or understand anything below this box.
:::

Argon2 is a secure password hashing algorithm.
It is designed to have both a configurable runtime as well as memory consumption.

This means that you can decide how long it takes to hash a password and how much memory is required.

In September 2021, Argon2 has been standardized by the IETF in {rfc}`9106`.

Argon2 comes in three variants: Argon2**d**, Argon2**i**, and Argon2**id**.
Argon2**d**'s strength is the resistance against [time–memory trade-offs], while Argon2**i**'s focus is on resistance against [side-channel attacks].

Accordingly, Argon2**i** was originally considered the correct choice for password hashing and password-based key derivation.
In practice it turned out that a *combination* of d and i -- that combines their strengths -- is the better choice.
And so Argon2**id** was born and is now considered the *main variant* (and the only variant required by the RFC to be implemented).


## Why “just use bcrypt” Is Not the Best Answer (Anymore)

The current workhorses of password hashing are unquestionably [*bcrypt*] and [PBKDF2].
And while they're still fine to use, the password cracking community embraced new technologies like [GPU]s and [ASIC]s to crack password in a highly parallel fashion.

An effective measure against extreme parallelism proved making computation of password hashes also *memory* hard.
The best known implementation of that approach is to date [*scrypt*].
However according to the [Argon2 paper] [^outdated], page 2:

> \[…\] the existence of a trivial time-memory tradeoff allows compact implementations with the same energy cost.

Therefore a new algorithm was needed.
This time future-proof and with committee-vetting instead of single implementors.

[^outdated]: Please note that the paper is in some parts outdated.
    For instance it predates the genesis of Argon2**id**.
    Generally please refer to {rfc}`9106` instead.


## Password Hashing Competition

The [Password Hashing Competition] took place between 2012 and 2015 to find a new, secure, and future-proof password hashing algorithm.
Previously the NIST was in charge but after certain events and [revelations] their integrity has been put into question by the general public.
So a group of independent cryptographers and security researchers came together.

In the end, Argon2 was [announced] as the winner.

[announced]: https://groups.google.com/forum/#!topic/crypto-competitions/3QNdmwBS98o
[argon2 paper]: https://www.password-hashing.net/argon2-specs.pdf
[asic]: https://en.wikipedia.org/wiki/Application-specific_integrated_circuit
[*bcrypt*]: https://en.wikipedia.org/wiki/Bcrypt
[gpu]: https://hashcat.net/hashcat/
[password hashing competition]: https://www.password-hashing.net/
[pbkdf2]: https://en.wikipedia.org/wiki/PBKDF2
[revelations]: https://en.wikipedia.org/wiki/Dual_EC_DRBG
[*scrypt*]: https://en.wikipedia.org/wiki/Scrypt
[side-channel attacks]: https://en.wikipedia.org/wiki/Side-channel_attack
[time–memory trade-offs]: https://en.wikipedia.org/wiki/Space–time_tradeoff
