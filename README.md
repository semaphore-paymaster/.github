# README.md

## Semaphore + Paymaster

### Project Overview

**Project Name:** Semaphore + Paymaster

**Description and Purpose:**
This project aims to integrate Semaphore with an ERC4337 compliant Paymaster to sponsor gas fees anonymously for Semaphore group members. The integration allows for the recovery of SemaphoreIdentity using an ERC4337 account and enforces periodic gas limits per user.

**Key Features:**
- **Gas Sponsorship:** Anonymously sponsor gas for Semaphore group members.
- **SemaphoreIdentity Recovery:** Allow recovery using an ERC4337 account.
- **Gas Limits:** Enforce periodic gas limits per user.
- **Gatekeeper Contract:** Manage Semaphore group membership using POAP tokens.

### Demonstration Video

<div style="position: relative; padding-bottom: 64.5933014354067%; height: 0;"><iframe src="https://www.loom.com/embed/67aa3d4d284c4e6294f00d6d852b4ad1?sid=70319082-cb91-4922-9d96-62aa38a46d16" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe></div>

### Repository References

- **.github:** [Link to Repository](https://github.com/semaphore-paymaster/.github)
- **maci-deployer:** [Link to Repository](https://github.com/semaphore-paymaster/maci-deployer)
- **frontend:** [Link to Repository](https://github.com/semaphore-paymaster/frontend)
- **wax:** [Link to Repository](https://github.com/semaphore-paymaster/wax)
- **maci-paymaster-example:** [Link to Repository](https://github.com/semaphore-paymaster/maci-paymaster-example)
- **semaphore:** [Link to Repository](https://github.com/semaphore-paymaster/semaphore)
- **mock-poap:** [Link to Repository](https://github.com/semaphore-paymaster/mock-poap)

### Usage Instructions

1. **Deploy the Paymaster and Gatekeeper Contracts:**
    - Follow the deployment steps to deploy both the Paymaster and Gatekeeper contracts.

2. **Add Members to Semaphore Group:**
    - Use the Gatekeeper contract to add members holding a specific POAP token to the Semaphore group.

3. **Sponsor Gas for Group Members:**
    - The Paymaster will automatically sponsor gas for any user operation with a valid Semaphore membership proof.

4. **Monitor Gas Limits:**
    - The Paymaster enforces periodic gas limits, ensuring each member can only use a specified amount of gas within each period.

### Credits and Acknowledgments

- Developed during the Brussels PSE Hackerhouse.
- Thanks to the Ethereum Foundation for the ERC4337 and Semaphore protocols.
- Special acknowledgments to the contributors and supporters of the project:
  - [zkfriendly](https://github.com/zkfriendly)
  - [jihoonsong](https://github.com/jihoonsong)
  - [baumstern](https://github.com/baumstern)
  - [brolag](https://github.com/brolag)

### License Information

This project is licensed under the MIT License. See the LICENSE file for more details.

---

### Technical Write-Up

#### TLDR;

- Integrate Semaphore with an ERC4337 compliant Paymaster.
- Anonymously sponsor gas for the Semaphore group members.
- Allow SemaphoreIdentity recovery using an ERC4337 account.
- Enforce periodic gas limits per user.

#### Introduction

This project, developed during the Brussels PSE Hackerhouse, resulted in implementing a Semaphore Paymaster. The Paymaster sponsors gas for any user operation with a valid Semaphore membership proof attached to its PaymasterData field. It also enforces periodic gas limits on how much gas can be used by each member during a given period. Membership of the Semaphore group is managed by a separate Gatekeeper contract that allows wallets holding a specific POAP to join the Semaphore group.

#### ERC 4337

ERC 4337 is a standard for smart contract-based wallets. A UserOperation is essentially the transaction a user intends to execute. All UserOperations are sent to the EntryPoint contract, which performs necessary checks and validations. The EntryPoint logic is extended with a Paymaster that decides whether to pay gas for executing a given UserOperation.

#### Semaphore Protocol

Semaphore allows the creation of on-chain groups with an Admin who can manage members. Members can send anonymous signals by providing membership proofs, with mechanisms to prevent double signaling using nullifiers. Even though nullifiers can be used as identifiers, they may be acceptable in some use-cases.

#### Simple Semaphore Paymaster Smart Contract

The ERC4337 Paymaster implements two methods, `_validatePaymasterUserOp` and `_postOp`. For `_validatePaymasterUserOp`:
1. Extract the Semaphore membership proof from the `paymasterAndData` field of the userOperation.
2. Verify the proof by passing it to the Semaphore contract.

---

For more details, refer to the code and comments within the repository.
