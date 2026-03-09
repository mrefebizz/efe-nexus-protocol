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
    subgraph "User Flow (Off-chain Interaction)" [User Flow (Off-chain Interaction)]
        User[User / Pioneer\n(Wallet/Interface)]
    end
    subgraph "On-Chain (Pi Testnet/Mainnet)" [On-Chain (Pi Testnet/Mainnet)]
        Vault[Vault Contract\n- Deposit π\n- Mint/Burn $EFE\n- Calls Policy]
        Policy[EfeNexusPolicy Contract\n- Fixed Peg: 1 $EFE = 3.14159 π\n- Conversion Functions]
        PiToken[PiToken\n(π Token - Pi Network native)]
        EFEToken[EFEToken\n($EFE Token - ERC-20 style)]
        efePiSwap[efePiSwap\n(Future DEX - Query Rates)]
    end

    User -->|Deposit π| Vault
    Vault -->|Mint $EFE| EFEToken
    Vault -->|Burn $EFE| User
    User -->|Redeem π| Vault
    Vault -->|Query Peg Logic| Policy
    Policy -->|Peg Logic --> $EFE Token| EFEToken
    Policy -->|Peg Logic --> PiToken| PiToken
    efePiSwap -->|Queries Policy for rates| Policy

    classDef dark fill:#222,stroke:#444,color:#eee;
    classDef component fill:#333,stroke:#888,color:#fff;
    class User dark;
    class Vault,Policy,PiToken,EFEToken,efePiSwap component;
    class On-chain dark;
    class User Flow dark;
