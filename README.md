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
