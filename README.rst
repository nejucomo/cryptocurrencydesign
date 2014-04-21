====================
cryptocurrencydesign
====================

Documenting design space for new cryptocurrencies.

Summary
=======

This document describes potential distinct (but perhaps non-orthogonal)
features, and the goals they strive to implement.

Much of the ideas here start as deltas from `bitcoin`_ design as a source
of inspiration.

.. _`bitcoin`: https://bitcoin.org/

Community
~~~~~~~~~

Please feel welcome to fork!  I value forks with diverging ideas over
spending much time arguing about merges.

Goals
=====

Goals are distinct and may be independent, mutually reinforcing, or
mutually exclusive.

Organizational Goals
~~~~~~~~~~~~~~~~~~~~

G: Consensual
-------------

No person or minority of participants has the ability to influence the
network behavior.  Participation is opt-in, by design.

Privacy Goals
-------------

G: User Privacy
...............

Users cannot be linked to accounts or ownership of currency.

G: User-Linked Accounts
.......................

Accounts are linked to users by some mechanism.

.. admonition:: example

  A system which ties accounts to smart cards issued by some
  identification authority would strive to achieve this goal.

Account Privacy
...............

G: User Identity Transparency
'''''''''''''''''''''''''''''

Every account can be publicly associated with a user's identity.

G: User Identity Privacy
''''''''''''''''''''''''

Accounts cannot be associated with user identity by anyone except that user.

G: Account Balance Transparency
'''''''''''''''''''''''''''''''

The balance of an account can be verified by anyone.

G: Account Balance Privacy
''''''''''''''''''''''''''

The balance of an account cannot be verified by anyone other than the account holder.

Transaction Privacy
...................

.. note:: In this section "sender" and "recipient" refer to accounts,
not users.  The association between users and accounts is separately
considered in `Account Privacy`_.

G: Transaction Sender Transparency
''''''''''''''''''''''''''''''''''

The sender of a transaction can be verified by any party.

G: Transaction Sender Privacy (Complete)
''''''''''''''''''''''''''''''''''''''''

The sender of a transaction cannot be verified by any party.

G: Transaction Sender Privacy (Partial)
'''''''''''''''''''''''''''''''''''''''

The sender of a transaction cannot be verified by any party other than
the recipient.

G: Transaction Recipient Transparency
'''''''''''''''''''''''''''''''''''''

The recipient of a transaction can be verified by any party.

G: Transaction Recipient Privacy
''''''''''''''''''''''''''''''''

The recipient of a transaction cannot be verified by any party other
than the sender.

G: Transaction Amount Transparency
''''''''''''''''''''''''''''''''''

The amount of currency in a transaction can be verified by any party.

G: Transaction Amount Privacy
'''''''''''''''''''''''''''''

The amount of currency in a transaction cannot be verified by any parties
aside from the sender and receiver.


Monetary Policy
~~~~~~~~~~~~~~~

G: Consistency
--------------

The rules of currency exchange are consistent in these ways:

#. Account balances may not be negative.
#. Transactions are consistent across accounts.

  + By implication, double spends are prohibited.

.. note:: The `bitcoin`_ blockchain design is eventually consistent
    because a double spend may cause a participants belief about an
    account balance to be retroactively altered.  By waiting for more
    proof-of-work verification this risk can be reduced.

G: Price Stability
------------------

The exchange price is stable relative to reference currencies.

G: Intrinsic Money Supply Evolution
-----------------------------------

The money supply grows and shrinks algorithmically based on intrinsic
network behavior, excluding the influence of (a minority of) users,
out out-of-network data.

G: Integral Money Supply Evolution
----------------------------------

The money supply grows and shrinks in reaction to the influence of data
external to the network, such as outside economic indicators or user votes.

G: Publicly Verifiable Monetary Supply
--------------------------------------

The number of currency units controlled by participants is publicly known.

.. note:: In `bitcoin`_, spends to nonsense addresses or lost private
    keys compromise this goal.


Disorganized Brainstorm
=======================

Alternative Double Spend Rules
------------------------------

Mal sends 1 BTC to Alice for a sandwich.  Then, Mal sends the same 1 BTC
(same outputs) to Bob for a soda.  Sometime later either Alice or Bob
suddenly lose their BTC as the consensus shifts away from the history
where they were paid.

If, instead, Mal sends 1 BTC to Alice for a sandwich and double spends
that 1 BTC back to Mal, then there is a chance that Mal retains control
over that BTC and gets a free sandwich.

What if, instead of any recipient of a transaction eventually retaining
double-spent coins, those coins have a different fate to lower Mal's
incentive to double-spend?

Double-Spend Records
....................

Let's suppose the offending transactions are both (or all) incorporated
into the block chain.  This allows future transactions to rely on
double-spends in some manner.

With bitcoin, all unspent outputs are valid, so we could preserve this
invariant by introducing a new "double spend record" which is a kind of
transaction that references offending outputs.  The outputs of this record
(if any) would preserve the invariant.  (Note: If there are zero outputs,
the invariant is still preserved.)

Destroyed Coins
...............

Perhaps the simplest rule is for the coins to be destroyed.  Who would
submit a double-spend record and why?

Paid to the Miner
.................

Another rule is that the double-spent coins are paid to the miner who
includes the double-spend record in their block.

This has a (possibly severe) drawback: miners would then be in a
privileged position and would be incentivized to double-spend more
than non-miners.

However, if Mal is not a miner, the trick of sending one of the
double-spends back to themself no longer provides any benefit.  In fact,
Mal loses 1 BTC regardless, so the only reason to do this is to spite
Alice.

If Mal is a miner, then the chance of recovering the double-spent coin is
directly proportional to the chance of mining *any block in the future*.

This is a deal breaker...  every miner could retroactively double-spend
all of their coins back to themselves by including double spend records
for all of their previous transactions on every mine attempt.
