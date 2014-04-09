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

Account Privacy
...............

G: Account Balance Privacy
''''''''''''''''''''''''''

The balance of an account cannot be verified by anyone other than the account holder.

Transaction Privacy
...................

G: Transaction Sender Privacy (Complete)
''''''''''''''''''''''''''''''''''''''''

The sender of a transaction cannot be verified by any party.

G: Transaction Sender Privacy (Partial)
'''''''''''''''''''''''''''''''''''''''

The sender of a transaction cannot be verified by any party other than
the recipient.

G: Transaction Recipient Privacy
''''''''''''''''''''''''''''''''

The recipient of a transaction cannot be verified by any party other
than the sender.

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

