# Gen Wealth - Generational Wealth Management Smart Contract

A Stacks blockchain smart contract designed to facilitate generational wealth building through collective contributions and Bitcoin stacking rewards.

## 🎯 Overview

Gen Wealth is a decentralized application that enables families or groups to pool STX tokens, participate in Bitcoin stacking, and distribute rewards across generations. The contract manages member contributions, stacking periods, and beneficiary distributions in a transparent and secure manner.

## ✨ Key Features

- **Member Management**: Admin-controlled membership system with contribution tracking
- **Collective Stacking**: Pool STX tokens for Bitcoin stacking with minimum lock periods
- **Generational Distribution**: Define beneficiaries for each generation
- **Secure Withdrawals**: Access controls for fund distribution
- **Transparent Tracking**: Full visibility of contributions and pool status

## 🏗️ Contract Architecture

### Core Constants
- **MEMBERS**: Maximum 5 members per generation
- **CONTRIBUTION-STX**: 30,000 micro-STX per contribution (~$300)
- **MINIMUM-CYCLE-DURATION**: 12 cycles (1 year minimum lock)
- **ADMIN**: Contract administrator address

### Data Structures
- `member-contributions`: Tracks total contributions and last payment per member
- `member-rights`: Manages active membership status
- `beneficiaries`: Maps generations to their beneficiary lists

### Contract State
- `total-pool`: Current STX pool balance
- `stacking-start-block`: Block when stacking began
- `is-stacking`: Current stacking status
- `current-generation`: Active generation number
- `locked-until`: Block when stacking period ends

## 🚀 Getting Started

### Prerequisites

- [Clarinet](https://github.com/hirosystems/clarinet) - Stacks smart contract development tool
- [Node.js](https://nodejs.org/) (v16 or higher)
- [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd gen_wealth
```

2. Install dependencies:
```bash
npm install
```

3. Verify Clarinet installation:
```bash
clarinet --version
```

### Development Setup

1. Check contract syntax:
```bash
clarinet check
```

2. Run tests:
```bash
npm test
```

3. Run tests with coverage:
```bash
npm run test:report
```

4. Watch mode for development:
```bash
npm run test:watch
```

## 📋 Contract Functions

### Admin Functions

#### `add-member`
Adds a new member to the contract.
```clarity
(add-member (member principal))
```

#### `start-stacking`
Initiates the stacking process with specified lock period.
```clarity
(start-stacking (lock-period uint))
```

#### `end-stacking`
Ends the stacking period (only after lock period expires).
```clarity
(end-stacking)
```

#### `set-next-generation`
Updates beneficiaries for the next generation.
```clarity
(set-next-generation (next-gen uint) (next-members (list 5 principal)))
```

### Member Functions

#### `contribute`
Allows active members to contribute STX to the pool.
```clarity
(contribute)
```

#### `withdraw-funds`
Allows authorized users to withdraw funds from the pool.
```clarity
(withdraw-funds (to principal) (amount uint))
```

### Read-Only Functions

#### `is-member`
Check if an address is an active member.
```clarity
(is-member (sender principal))
```

#### `get-total-pool`
Get current pool balance.
```clarity
(get-total-pool)
```

#### `get-beneficiaries`
Get beneficiaries for a specific generation.
```clarity
(get-beneficiaries (generation uint))
```

#### `can-access-fund`
Check if a user can access funds.
```clarity
(can-access-fund (user principal))
```

## 🔒 Security Features

- **Admin Controls**: Critical functions restricted to admin address
- **Member Verification**: Only active members can contribute
- **Access Controls**: Fund withdrawals limited to admin and current generation beneficiaries
- **Stacking Protection**: Funds locked during stacking periods
- **Balance Validation**: Withdrawal amounts validated against available pool

## 🧪 Testing

The project uses Vitest with Clarinet SDK for comprehensive testing:

```bash
# Run all tests
npm test

# Run tests with coverage and cost analysis
npm run test:report

# Watch mode for continuous testing
npm run test:watch
```

Test files are located in the `tests/` directory and use TypeScript for type safety.

## 📁 Project Structure

```
gen_wealth/
├── contracts/
│   └── gen_wealth.clar          # Main smart contract
├── tests/
│   └── gen_wealth.test.ts       # Test suite
├── settings/
│   ├── Devnet.toml             # Development network config
│   ├── Testnet.toml            # Testnet configuration
│   └── Mainnet.toml            # Mainnet configuration
├── Clarinet.toml               # Clarinet project configuration
├── package.json                # Node.js dependencies and scripts
├── tsconfig.json               # TypeScript configuration
├── vitest.config.js            # Test configuration
└── README.md                   # This file
```

## 🌐 Deployment

### Testnet Deployment

1. Configure testnet settings in `settings/Testnet.toml`
2. Deploy using Clarinet:
```bash
clarinet deployments generate --testnet
clarinet deployments apply --testnet
```

### Mainnet Deployment

1. Configure mainnet settings in `settings/Mainnet.toml`
2. Deploy using Clarinet:
```bash
clarinet deployments generate --mainnet
clarinet deployments apply --mainnet
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/new-feature`
3. Make your changes and add tests
4. Run the test suite: `npm test`
5. Commit your changes: `git commit -am 'Add new feature'`
6. Push to the branch: `git push origin feature/new-feature`
7. Submit a pull request

## 📄 License

This project is licensed under the ISC License - see the LICENSE file for details.

## ⚠️ Disclaimer

This smart contract is for educational and experimental purposes. Always conduct thorough testing and security audits before deploying to mainnet with real funds.

## 📞 Support

For questions, issues, or contributions, please open an issue on the GitHub repository.
