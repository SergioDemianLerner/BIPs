<pre>
  BIP: 200
  Title: Block size increase to 2MB coupled with Segwit activation
  Authors: Sergio Demian Lerner
  Status: Draft
  Type: Standards Track
  Created: 2017-07-01
</pre>

==Abstract==

This BIPs describes a one-time increase in the maximum non-witness block size from 1MB to 2MB, triggered by the activation of segwit as of BIP91, but delayed approximately 3 months after segwit activation.

To prevent DoS attacks, transaction serialized size is limited to 1,000,000 bytes, excluding witness data.

==Motivation==

# Enabling Segwit
# Reducing temporarily the fee pressure until other scaling techniques such as the Lighntning Network, sidechains, drivechains and extension blocks prove to be useful or not for Bitcoin scaling.
# Maximum transacttion size is kept, to maximize compatibility with current software and prevent algorithmic and data size DoS's.

==Specification==

# The plain block size is defined as the serialized block size without witness programs.
# Deploy a modified BIP91 to activate Segwit. The only modification is that the signal "segsignal" is replaced by "segwit2x".
# If Segwit activates at block N via bit 4, then block N+12960 activates a new plain block size limit of 2 MB (2,000,000 bytes). In this case, at block N+12960 a hard-fork occurs.
# The block that activates the hard-fork must have a plain block size greater than 1 MB.
# To allow reception of larger blocks, MAX_PROTOCOL_MESSAGE_LENGTH is set to 8,000,000 bytes. This is the highest size of a block when serialized with witness-programs.
# After activation, the maximum size of a compact block shorttxids plus prefilledtxn is increased from 400,000 to 800,000.
# A MAX_TX_BASE_SIZE is defined as 1,000,000 bytes.
# Any transaction with a non-witness serialized size exceeding MAX_TX_BASE_SIZE is invalid.


==Backward compatibility==

Older clients are not compatible with this change.  The first block exceeding 1,000,000 bytes will partition older clients off the new network.

==Discussion==

In the short term, an increase is needed to continue to facilitate
network growth, and buy time for more comprehensive solutions to be
developed and tested, such as the Lightning Network, sidechains, drivechains and extension blocks.
This reduces the fee pressure on users and companies creating on-chain transactions, matching market expectations and preventing further market disruption.


==Implementation==

https://github.com/btc1/bitcoin branch segwit2x

