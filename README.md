# ChainDiversify

ChainDiversify is a decentralized protocol that enables users to invest in a vault on a single chain, while the smart contract handles cross-chain investments using Wormhole and Stargate functionalities. This simplifies the process of managing and tracking investments across multiple chains and protocols, providing users with a seamless experience in maximizing their yield.

## Overview

- **Cross-Chain Investments**: ChainDiversify leverages Wormhole and Stargate to bridge funds across different blockchain networks, enabling users to tap into higher yield opportunities without the complexity of manual bridging and management.
- **Single Vault Management**: Users can deposit assets into a single vault on the primary chain. The smart contract then handles the distribution and management of these funds across various chains and yield-generating protocols.
- **Epoch-Based Operation**: The protocol operates in defined epochs. During an epoch, funds are allocated across various protocols and chains, and at the end of the epoch, the returns are collected and made available for withdrawal.
- **Security**: The contract utilizes OpenZeppelin's libraries for security features such as reentrancy protection and safe ERC20 operations.

## Contracts

### CrossChain Contract

This contract manages the core functionality of the ChainDiversify protocol. It handles deposits, withdrawals, cross-chain transfers, and interactions with yield-generating vaults on other chains.

#### Key Variables
- `epochRunning`: Indicates if an epoch is currently active.
- `token`: The address of the ERC20 token managed by the contract.
- `vault`: The address of the primary vault on the main chain.
- `nOwner`: The address of the contract owner.
- `riveraVault`: The address of the yield-generating vault on another chain.
- `stargate`: The address of the Stargate router for cross-chain swaps.
- `wormholeRelayer`: The address of the Wormhole relayer for cross-chain messaging.

#### Key Functions
- `deposit()`: Allows the vault to deposit tokens into the contract.
- `withdraw(uint256 _amount)`: Allows the vault to withdraw a specified amount of tokens, provided that no epoch is currently running.
- `startEpoch(address _reci, uint16 targetChain)`: Starts a new epoch, bridging funds to other chains and investing them in yield protocols.
- `endEpoch()`: Ends the current epoch, collects the returns, and makes them available for withdrawal.
- `balanceOf()`: Returns the balance of the tokens in the contract.
- `redeemEth()`: Allows the owner to redeem any ETH held by the contract.

## Getting Started

To deploy and interact with the ChainDiversify protocol:

1. **Deployment**: Deploy the `CrossChain` contract by providing the necessary parameters such as token address, Rivera vault, Stargate, and Wormhole addresses, and the target chain ID.
2. **Set Vault**: Once deployed, set the primary vault address using the `setVaults(address _vault)` function.
3. **Start an Epoch**: Use the `startEpoch(address _reci, uint16 targetChain)` function to start a new investment epoch. The contract will automatically bridge and invest funds.
4. **End an Epoch**: Conclude the investment period by calling `endEpoch()`. This will bring back the investments and make the returns available.
5. **Withdraw**: Withdraw the funds from the contract back to the vault using the `withdraw(uint256 _amount)` function.

## Security Considerations

- **Reentrancy Guard**: The contract uses `ReentrancyGuard` to protect against reentrancy attacks.
- **SafeERC20**: Token transfers are handled using OpenZeppelin’s `SafeERC20` to ensure secure operations.
- **Pausable**: The contract includes mechanisms to pause operations in case of an emergency, ensuring user funds are safeguarded.

## License

This project is licensed under the UNLICENSED License.
