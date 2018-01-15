Mun Core version 0.1.0.3
========================

Release is now available from:

  <https://www.mun.org/downloads/#wallets>

This is a new minor version release, bringing various bugfixes and other
improvements.

Please report bugs using the issue tracker at github:

  <https://github.com/munpay/mun/issues>


Upgrading and downgrading
=========================

How to Upgrade
--------------

If you are running an older version, shut it down. Wait until it has completely
shut down (which might take a few minutes for older versions), then run the
installer (on Windows) or just copy over /Applications/Mun-Qt (on Mac) or
mund/mun-qt (on Linux).

Downgrade warning
-----------------

### Downgrade to a version < 0.12.2.2

Because release 0.12.2.2 included the [per-UTXO fix](release-notes/dash/release-notes-0.12.2.2.md#per-utxo-fix)
which changed the structure of the internal database, you will have to reindex
the database if you decide to use any pre-0.12.2.2 version.

Wallet forward or backward compatibility was not affected.

### Downgrade to 0.12.2.2

Downgrading to 0.12.2.2 does not require any additional actions, should be
fully compatible.

Notable changes
===============

InstantSend fixes
-----------------

Coin selection could work slightly incorrect in some edge cases which could
lead to a creation of an InstantSend transaction which only the local wallet
would consider to be a good candidate for a lock. Such txes was not locked by
the network but they were creating a confusion on the user side giving an
impression of a slightly higher InstantSend failure rate.

Another issue fixed in this release is that masternodes could vote for a tx
that is not going to be accepted to the mempool sometimes. This could lead to
a situation when user funds would be locked even though InstantSend transaction
would not show up on the receiving side.

Fix -liquidityprovider option
-----------------------------

Turned out that liquidityprovider mixing mode practically stopped working after
recent improvements in the PrivateSend mixing algorithm due to a suboptimal
looping which occurs only in this mode (due to a huge number of rounds). To fix
the issue a small part of the mixing algorithm was reverted to a pre-0.12.2 one
for this mode only. Regular users were not affected by the issue in any way and
will continue to use the improved one just like before.

Other improvements and bug fixes
--------------------------------

This release also fixes a few crashes and compatibility issues.


0.12.2.3 Change log
===================

See detailed [change log](https://github.com/dashpay/dash/compare/v0.12.2.2...dashpay:v0.12.2.3) below.

### Backports:
- [`068b20bc7`](https://github.com/dashpay/dash/commit/068b20bc7) Merge #8256: BUG: bitcoin-qt crash
- [`f71ab1daf`](https://github.com/dashpay/dash/commit/f71ab1daf) Merge #11847: Fixes compatibility with boost 1.66 (#1836)

### PrivateSend:
- [`fa5fc418a`](https://github.com/dashpay/dash/commit/fa5fc418a) Fix -liquidityprovider option (#1829)
- [`d261575b4`](https://github.com/dashpay/dash/commit/d261575b4) Skip existing masternode conections on mixing (#1833)
- [`21a10057d`](https://github.com/dashpay/dash/commit/21a10057d) Protect CKeyHolderStorage via mutex (#1834)
- [`476888683`](https://github.com/dashpay/dash/commit/476888683) Avoid reference leakage in CKeyHolderStorage::AddKey (#1840)

### InstantSend:
- [`d6e2aa843`](https://github.com/dashpay/dash/commit/d6e2aa843) Swap iterations and fUseInstantSend parameters in ApproximateBestSubset (#1819)
- [`c9bafe154`](https://github.com/dashpay/dash/commit/c9bafe154) Vote on IS only if it was accepted to mempool (#1826)

### Other:
- [`ada41c3af`](https://github.com/dashpay/dash/commit/ada41c3af) Fix crash on exit when -createwalletbackups=0 (#1810)
- [`63e0e30e3`](https://github.com/dashpay/dash/commit/63e0e30e3) bump version to 0.12.2.3 (#1827)

Credits
=======

Thanks to everyone who directly contributed to this release:

- Alexander Block
- lodgepole
- UdjinM6

