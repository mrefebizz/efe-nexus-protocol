# Efe Nexus Protocol

**Immutable Fixed Peg on Pi Network**  
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

## Current Contracts

| Contract            | Purpose                          | Status       | Testnet ID (TBD) |
|---------------------|----------------------------------|--------------|------------------|
| EfeNexusPolicy      | Peg enforcement & conversions    | Prototype    | —                |

## Build & Deploy (Pi Testnet)

1. Install Soroban CLI:

2. ````markdown name=efe-nexus-mermaid.md
```mermaid
%% Efe Nexus Protocol Architecture Diagram (dark-theme friendly)
%% NOTE: Use "architecture-beta" or "flowchart" as preferred; this uses flowchart for compatibility.

flowchart TB
  %% Groups (subgraphs)
  subgraph User Flow ["User Flow (Off-chain Interaction)"]
    User[User<br/>(Wallet/Interface)]
  end

  subgraph On-chain ["On-Chain (Pi Testnet/Mainnet)"]
    Vault[Vault Contract<br/>- Deposit π<br/>- Mint/Burn $EFE<br/>- Calls Policy]
    Policy[EfeNexusPolicy Contract<br/>- Fixed Peg:<br/>1 $EFE = 3.14159 π<br/>- Conversion Functions]
    PiToken[π Token<br/>(Pi Network native)]
    EFEToken[$EFE Token<br/>(ERC-20 style)]

    %% DEX stub for future
    efePiSwap[efePiSwap DEX<br/>(Queries Policy for rates)]
  end

  %% Flows
  User -->|Deposit π| Vault
  Vault -->|Mint $EFE| EFEToken
  Vault -->|Burn $EFE| EFEToken
  Vault -->|Redeem π| PiToken
  Vault -- Calls --> Policy
  Policy -- Peg Logic --> EFEToken
  Policy -- Peg Logic --> PiToken

  %% DEX future use
  efePiSwap -- "Query Rates" --> Policy

  %% Group styling for dark theme
  classDef dark fill:#222,stroke:#444,color:#eee;
  classDef component fill:#333,stroke:#888,color:#fff;
  class User dark;
  class Vault,Policy,PiToken,EFEToken,efePiSwap component;
  class On-chain dark;
  class User Flow dark;

  %% Extra labels for PiRC1, Mainnet/Testnet
  On-chain:::dark
```
````
