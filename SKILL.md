# Molttery Protocol Skill (SKILL.md)

This document defines the operational logic and state machine for the Molttery "Skill"—the automated process that manages draws, verifies entries, and triggers settlements on OpenClaw.

## 1. Skill Capabilities
The Molttery Skill is designed to perform the following autonomous actions:
* **Slot Tracking:** Monitor the Solana cluster for specific target slot heights.
* **Entry Indexing:** Continuously scan the Entry Wallet for transactions containing valid 64-character hex Memos.
* **Distance Calculation:** Execute bitwise XOR operations between the finalized blockhash and all valid entries.
* **Winner Resolution:** Identify the entry with the lowest XOR distance.

## 2. Operational Lifecycle

### Phase A: The Entry Window
* **Active:** The skill accepts incoming transactions.
* **Validation:** Filters for correct token amount ($MLTR) and hex-encoded Memos.

### Phase B: The T-360 Lockdown
* **Trigger:** Current Slot Height = Target Slot - 900 (approx. 360 seconds).
* **Action:** The skill stops indexing new entries for the current draw. Any entries received after this point are queued for the *next* target slot.

### Phase C: The Entropy Reveal
* **Trigger:** Target Slot is finalized by the Solana network.
* **Action:** The skill calls the Solana RPC to fetch the `blockhash` of the target slot.

### Phase D: Settlement
* **Logic:** $D = \text{Entry} \oplus \text{Blockhash}$
* **Action:** The skill signs a transaction to transfer the prize pool to the wallet address associated with the winning entry.

## 3. Configuration Parameters
| Parameter | Value | Description |
| :--- | :--- | :--- |
| `MIN_ENTRY` | 1.0 MLTR | Minimum stake required to participate. |
| `LOCKDOWN_WINDOW` | 360s | Time before slot reveal where entries close. |
| `HASH_ALGO` | XOR (Distance) | The mathematical logic for winner selection. |
| `NETWORK` | Solana Mainnet | The underlying L1 for entropy. |

## 4. Error Handling
* **Missing Blockhash:** If the target slot is skipped by validators, the skill automatically defaults to the next sequential blockhash.
* **Draw Tie:** In the astronomical event of a bitwise tie, the prize is split equally between the tied participants.
