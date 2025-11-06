# Auction-using-Solidity

Overview:

This project implements a decentralized auction system using Solidity on the Ethereum blockchain. The smart contract allows users to participate in an auction by placing bids securely, ensuring transparency and immutability through blockchain technology.
The auction lifecycle includes creation, bidding, cancellation, and finalization — with automatic fund handling and refund logic built in.


Features:

Auction Lifecycle Management — Supports starting, running, ending, and canceling auctions.

Secure Bidding System — Tracks each participant’s total bid and determines the highest binding bid.

Ownership Control — Only the contract owner can cancel or finalize the auction.

Block-based Timers — Auction duration is defined using Ethereum block numbers.

Automatic Payouts — Handles refunds and payments automatically upon auction finalization.

IPFS Integration Ready — ipfsHash variable allows linking to off-chain metadata or item descriptions.


Smart Contract Details:

Contract Name- Auction

| Variable                  | Type                       | Description                                                  |
| ------------------------- | -------------------------- | ------------------------------------------------------------ |
| `owner`                   | `address payable`          | The auction creator and contract owner.                      |
| `startBlock` / `endBlock` | `uint`                     | Define the auction’s time window in block numbers.           |
| `auctionState`            | `enum State`               | Tracks auction state — Started, Running, Ended, or Canceled. |
| `highestBindingBid`       | `uint`                     | The current highest valid bid amount.                        |
| `highestBidder`           | `address payable`          | Address of the leading bidder.                               |
| `bids`                    | `mapping(address => uint)` | Tracks each participant’s total bids.                        |


Functions:

| Function              | Description                                                                         |
| --------------------- | ----------------------------------------------------------------------------------- |
| `placeBid()`          | Allows users (except the owner) to place or increase their bids during the auction. |
| `cancelAuction()`     | Lets the owner cancel the auction before it ends.                                   |
| `finalizeAuction()`   | Transfers funds to the correct participants once the auction ends or is canceled.   |
| `min(uint a, uint b)` | Internal utility function to return the smaller of two values.                      |


How It Works:

1] Auction Initialization-

The auction is automatically started upon contract deployment with a duration of 100 blocks.

2] Bidding Phase-

Participants can place bids using placeBid().

Each bid must exceed the current highestBindingBid.

Bids are cumulative and tracked per user.

3] Ending or Canceling-

The auction ends automatically after the end block.

The owner can also cancel it manually.

4] Finalization-

The highest bidder wins and pays the highest binding bid.

All other participants receive refunds automatically.

If canceled, everyone gets a full refund.


Deployment:

Prerequisites

https://nodejs.org/en

https://remix.ethereum.org/

https://metamask.io/


Steps:

1] Compile the contract using Hardhat or Remix.

2] Deploy it to a testnet (e.g., Sepolia or Goerli).

3] Interact via the deployed address using Remix or a frontend DApp.


Future Improvements:

-> Integrate with IPFS to display auction item details.

-> Add frontend UI for real-time bidding using React and Ethers.js.

-> Implement dynamic bid increments and multiple-item auctions.
