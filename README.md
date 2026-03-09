# Efe Nexus Protocol

Immutable Fixed Peg on Pi Network  
1 $EFE = 3.14159 π — mathematically enforced, no oracles, no governance changes.

Pure Soroban smart contract implementing a rock-solid peg for the Efe Nexus ecosystem (@EfeNexus on X).  
- Mint $EFE by depositing π  
- Redeem π by burning $EFE  
- Designed for vaults, swaps, staking with predictable utility value

## Alignment with PiRC1 (Pi Ecosystem Token Design)

This project follows the spirit of **PiRC1** (https://github.com/PiNetwork/PiRC/tree/main/PiRC1):  
- Utility-first: Peg ensures stable, real-world value over speculation  
- On-chain transparency & immutability: No upgrade keys, pure view functions  
- Community-oriented mechanics: Deposit/burn enables participation without volatility risks  

See [docs/alignment-with-pirc1.md](docs/alignment-with-pirc1.md) for detailed mapping to PiRC1 sections (vision, core design, participation).

## Architecture Overview

```mermaid
flowchart TB
    subgraph user_flow["User Flow (Off-chain)"]
        direction TB
        User["User\n(Pioneer / Wallet / Interface)"]
    end

    subgraph on_chain["On-Chain (Pi Testnet / Mainnet)"]
        direction TB
        Vault["EfePiVault Contract\n- Deposit π\n- Mint / Burn $EFE\n- Calls Policy"]
        Policy["EfeNexusPolicy Contract\n- Immutable Peg: 1 $EFE = 3.14159 π\n- Conversion Functions"]
        PiToken["π Token\n(Pi Network native)"]
        EfeToken["$EFE Token\n(ERC-20 style on Soroban)"]
        Swap["efePiSwap\n(Future DEX)\nQueries Policy for rates"]
    end

    User -->|Deposit π| Vault
    Vault -->|Mint $EFE| EfeToken
    Vault -->|Burn $EFE| User
    User -->|Redeem π| Vault
    Vault -->|Query Peg Rate| Policy
    Policy -->|Peg Logic → $EFE| EfeToken
    Policy -->|Peg Logic → π| PiToken
    Swap -->|Query Rates| Policy

    classDef darkGroup fill:#1e293b,stroke:#475569,stroke-width:2px,color:#e2e8f0
    classDef component fill:#334155,stroke:#64748b,color:#f1f5f9
    classDef user fill:#475569,stroke:#94a3b8,color:#e2e8f0

    class user_flow,on_chain darkGroup
    class User user
    class Vault,Policy,PiToken,EfeToken,Swap component
