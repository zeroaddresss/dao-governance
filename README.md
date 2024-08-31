# 🏛️ Governance DAO

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Solidity](https://img.shields.io/badge/Solidity-^0.8.18-e6e6e6?logo=solidity)](https://docs.soliditylang.org/en/v0.8.18/)
[![OpenZeppelin](https://img.shields.io/badge/OpenZeppelin-5.0.0-blue?logo=openzeppelin)](https://www.openzeppelin.com/)

A robust and flexible Decentralized Autonomous Organization (DAO) governance system, leveraging OpenZeppelin's smart contract libraries.

## 🌟 Key Features

- **On-chain Governance**: Fully decentralized decision-making process
- **Time-locked Execution**: Enhanced security with delayed implementation of proposals
- **Flexible Voting**: Customizable voting periods and thresholds
- **ERC20 Governance Token**: Built-in token for voting power allocation
- **Upgradeable Architecture**: Prepared for future improvements and adaptations

## 🚀 Quick Start

### Prerequisites

- [Foundry](https://book.getfoundry.sh/getting-started/installation.html)
- [Node.js](https://nodejs.org/) (v14+ recommended)

### Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/zeroaddresss/governance-dao.git
   cd governance-dao
   ```

2. Install dependencies:
   ```bash
   forge install
   ```

3. Compile the contracts:
   ```bash
   forge build
   ```

4. Run tests:
   ```bash
   forge test
   ```

## 📚 Detailed Documentation

### Smart Contracts

1. **MyGovernor.sol**: The core governance contract that manages proposals, voting, and execution.
2. **TimeLock.sol**: Implements a delay mechanism for executing approved proposals.
3. **GovToken.sol**: ERC20 token with voting capabilities for governance participation.
4. **Box.sol**: A simple contract demonstrating governance-controlled state changes.

### Governance Process

1. **Proposal Creation**: Any token holder can create a proposal.
2. **Voting**: Token holders cast their votes during the voting period.
3. **Execution**: If approved, proposals are queued and then executed after a time delay.

### Configuration

Key parameters in `MyGovernor.sol`:
- Voting Delay: 1 block
- Voting Period: 50400 blocks (≈1 week on Ethereum mainnet)
- Proposal Threshold: 0 tokens
- Quorum: 4% of total supply

These can be adjusted based on your DAO's specific needs.

## 🎬 Examples and Use Cases

### Creating a Proposal

```sol
function propose(
    address[] memory targets,
    uint256[] memory values,
    bytes[] memory calldatas,
    string memory description
) public returns (uint256)
```

Example:
```solidity
address[] memory targets = new address[](1);
targets[0] = address(boxContract);

uint256[] memory values = new uint256[](1);
values[0] = 0;

bytes[] memory calldatas = new bytes[](1);
calldatas[0] = abi.encodeWithSignature("store(uint256)", newValue);

string memory description = "Set Box value to " + newValue;

uint256 proposalId = governor.propose(targets, values, calldatas, description);
```

### Casting a Vote

```solidity
function castVote(uint256 proposalId, uint8 support) public returns (uint256)
```

Example:
```solidity
uint256 proposalId = /* ... */;
uint8 support = 1; // 0 = Against, 1 = For, 2 = Abstain
governor.castVote(proposalId, support);
```

## 📁 Project Structure

```
governance-dao/
├── src/
│   ├── MyGovernor.sol
│   ├── TimeLock.sol
│   ├── GovToken.sol
│   └── Box.sol
├── test/
│   └── MyGovernorTest.t.sol
├── script/
└── README.md
```

## 🛠 Dependencies

- OpenZeppelin Contracts ^5.0.0
- Foundry (for development and testing)

## 🧪 Testing

Run the test suite using Foundry:

```bash
forge test
```

For more detailed output:

```bash
forge test -vvvvv
```

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
