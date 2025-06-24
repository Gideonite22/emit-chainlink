# Emit Chainlink: Decentralized Oracle Data Feed Management

A robust, secure Chainlink data feed emission and management system, enabling transparent and verifiable oracle data transmission across blockchain networks.

## Overview

Emit Chainlink is a blockchain-based platform that serves decentralized oracle infrastructure by providing:
- Immutable oracle data feed registration
- Verifiable data attribution and transmission tracking
- Flexible access control for data feeds
- Governance system for oracle network management
- Monetization options for premium data feeds

The platform connects data providers, blockchain developers, and oracle network participants in a trustless environment where data integrity and secure transmission are guaranteed by blockchain technology.

## Architecture

The system is built around a primary smart contract that manages:

```mermaid
graph TD
    A[Data Providers] -->|Register| B[Emit Chainlink Contract]
    B -->|Manages| C[Data Feeds]
    B -->|Controls| D[Access Permissions]
    B -->|Tracks| E[Feed Transmissions]
    B -->|Facilitates| F[Governance]
    C -->|Types| G[Public/Paid/Permissioned]
    H[Users/Contracts] -->|Access| C
    H -->|Vote on| F
```

### Core Components:
- Data Provider Registry
- Data Feed Management
- Access Control System
- Transmission Tracking
- Governance Mechanism

## Contract Documentation

### emit-chainlink.clar

The main contract handling core functionality of the Emit Chainlink oracle platform.

#### Key Features:
- Data provider registration and verification
- Data feed registration and metadata storage
- Flexible access control (Public, Paid, Permissioned)
- Transmission tracking and attribution
- Governance proposal system

#### Access Types:
- `ACCESS-TYPE-PUBLIC` (u1): Freely accessible feeds
- `ACCESS-TYPE-PAID` (u2): Requires payment for access
- `ACCESS-TYPE-PERMISSIONED` (u3): Requires explicit permission

## Getting Started

### Prerequisites
- Clarinet
- Stacks wallet for deployment/interaction

### Basic Usage

1. Register as a researcher:
```clarity
(contract-call? .ocean-vault register-researcher "John Doe" "Marine Institute" "PhD Marine Biology")
```

2. Register a dataset:
```clarity
(contract-call? .ocean-vault register-dataset 
    "dataset-001"
    "Coral Reef Survey 2023"
    "Environmental Data"
    "Great Barrier Reef"
    u1683849600
    "Standard sampling methodology"
    0x... ;; data hash
    u1    ;; open access
    u0    ;; free
)
```

3. Access a dataset:
```clarity
(contract-call? .ocean-vault check-dataset-access "dataset-001" tx-sender)
```

## Function Reference

### Public Functions

#### Researcher Management
- `register-researcher`: Register a new researcher
- `get-researcher`: Retrieve researcher information

#### Dataset Management
- `register-dataset`: Register a new dataset
- `verify-dataset`: Verify a dataset (admin only)
- `get-dataset`: Retrieve dataset information

#### Access Control
- `grant-dataset-access`: Grant access to permissioned dataset
- `access-paid-dataset`: Purchase access to paid dataset
- `check-dataset-access`: Check access permissions

#### Citations
- `cite-dataset`: Cite a dataset in research
- `get-citation`: Retrieve citation information

#### Governance
- `create-proposal`: Create a governance proposal
- `vote-on-proposal`: Vote on active proposals
- `finalize-proposal`: Finalize proposal after voting period

## Development

### Testing
1. Clone the repository
2. Install Clarinet
3. Run tests:
```bash
clarinet test
```

### Local Development
1. Start Clarinet console:
```bash
clarinet console
```
2. Deploy contracts:
```clarity
(contract-call? .ocean-vault ...)
```

## Security Considerations

### Access Control
- Only registered researchers can register datasets
- Dataset access is strictly controlled based on type
- Paid access requires successful STX transfer
- Permission grants only by dataset owners

### Governance
- Only registered researchers can participate
- Proposals have fixed voting periods
- Vote counting is transparent and immutable
- Status changes are permanent once finalized

### Limitations
- On-chain storage limited to metadata
- Actual dataset storage should be off-chain
- Access control applies to metadata only
- Citations must be by registered researchers