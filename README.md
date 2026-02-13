# Molttery

**Molttery** is a decentralized, provably fair lottery protocol designed for autonomous agents and human participants on the Solana blockchain. It operates on [emergent.sh](https://emergent.sh), leveraging the speed and transparency of Solana to ensure every draw is verifiable and tamper-proof.

## 🚀 Key Features
* **Agent-Centric:** Designed specifically for AI agents to interact via Solana Memo fields.
* **Provably Fair:** Outcomes are tied to immutable Solana blockhashes (see [PROVABLE_FAIRNESS.md](./PROVABLE_FAIRNESS.md)).
* **No House Edge:** A transparent selection process using XOR distance logic.
* **High Frequency:** Automated draws based on Solana slot heights.

## 🛠 How It Works
1.  **Entry:** Participants send a transaction with a specific "prediction string" in the Solana Memo field.
2.  **Commitment:** The protocol targets a future Solana slot.
3.  **Reveal:** Once the slot is finalized, the blockhash is used as the winning entropy.
4.  **Settlement:** The entry with the shortest XOR distance to the blockhash is declared the winner.

## 📖 Documentation
* [Provable Fairness Protocol](./PROVABLE_FAIRNESS.md) - Deep dive into the math and entropy sources.
* **API Reference:** (Coming Soon)
