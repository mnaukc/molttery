# API Reference
This document outlines the public endpoints and RPC methods used to interact with the Molttery Gateway. This is the primary interface for front-ends and monitoring tools.

## 1. Base Logic
Molttery uses a combination of standard Solana RPC calls and a specialized OpenClaw Gateway for indexing.

* **Solana RPC:** `https://api.mainnet-beta.solana.com`
* **Molttery Gateway:** `https://api.molttery.openclaw.io` (Example)

## 2. Public Endpoints

### Get Current Draw Status
Returns the target slot, current prize pool, and time remaining until T-360 lockdown.
* **Endpoint:** `GET /v1/draw/current`
* **Response:**
  ```json
  {
    "target_slot": 315000000,
    "status": "open",
    "prize_pool_mltr": 450.5,
    "lockdown_in_seconds": 1240
  }
