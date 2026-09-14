# Get a pre-fork coin onto Blake2b without moving your real bitcoin

Short guide · September 2026  
Not financial advice. Practice with a tiny amount first.

## Three sentences

If you held bitcoin **yourself** before block **961,640**, that same coin now exists on **two chains**: Bitcoin and Blake2b.

A normal send from the old wallet is valid on **both**. Then the Blake2b copy is gone even though you only meant to move bitcoin — or the other way around.

So spend **Blake2b first**, with a signature Bitcoin will reject (`0x21`). Only after that, move the bitcoin side separately.

If you had **no** bitcoin before the fork, there is nothing to claim here.

## What you need

- The old coin in a wallet whose seed **you** hold (not an exchange)
- Bitcoin Knots **29.4.1.knots20260508** or newer — that node follows Blake2b
- **Shrike** (a Sparrow offshoot). Normal Sparrow cannot make the special signature
- Lookups: [mempool.guide](https://mempool.guide) = Blake2b, [mempool.space](https://mempool.space) = Bitcoin  
  Do not mix them up.

## Do this

1. **Use a tiny coin.** Not the big pile. Test first.
2. **Open two windows.** Left: Shrike + Knots (Blake2b). Right: your normal bitcoin wallet. The same coin must still show on **both**.
3. **Make a new receive address in Shrike.** Seed on paper, offline. That address is only the destination — it does not protect you by itself.
4. **Send only that one coin** in Shrike to the new address (value minus fee).
5. **On the send screen look for `0x21` or “replay protected”.** If it is not there, do not send.
6. **Send only through Knots or mempool.guide.** Not mempool.space. Not a bitcoin-connected Sparrow.
7. **Wait until it confirms.** Then check Bitcoin: the old coin must **still be there**. If it is gone on Bitcoin too, the payment was copied. Stop.
8. **Only now** move the bitcoin coin, if you want. That send can be a normal one.

## Do not send if

- there is no `0x21` on the screen
- you are about to paste the hex into mempool.space or a bitcoin wallet
- several coins are mixed and one of them exists on only one chain
- this is the first try and the amount is not tiny
- a hardware wallet cannot make the special signature

## Check afterwards

| | Blake2b (mempool.guide) | Bitcoin (mempool.space) |
|---|---|---|
| The old coin | gone, spent by your new payment | still there |
| The new address | has the amount | ignore |
| The signature | ends in `21` | the Blake2b payment is rejected or missing |

## Software

- Node: [bitcoinknots.org](https://bitcoinknots.org) — check the file hashes. Bitcoin Core follows the **other** chain.
- Wallet: [Shrike](https://shrikewallet.com) — unofficial, not audited, check the hashes.
- Do not use public Electrum servers from before the fork. They stop on the old chain.

## If Shrike is not an option (worse plan B)

Normal Sparrow cannot set `0x21`. Some people set a **locktime** in Sparrow → Details to a block height Blake2b already passed and Bitcoin has not. Copy the hex. Send it only on Blake2b.

That is a **delay**, not a real split. Later the same hex can become valid on Bitcoin. Do not try this on a large amount.

## How it goes wrong

- The wallet is looking at Bitcoin and sends the payment there
- Old signature (`0x01`) — valid on both chains
- You spent Bitcoin first — that copy can be replayed onto Blake2b
- First move is a deposit to an exchange — you do not control which chain they credit
- You only made a new address and thought that was enough
