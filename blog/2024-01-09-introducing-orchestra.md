---
slug: introducing-orchestra-multichain-deployment-made-easy
title: Introducing Orchestra — Multi-chain Contract Deployment Made Easy
authors:
    - taek
    - derek
hide_table_of_contents: true
---

# Introducing Orchestra — Multi-chain Contract Deployment Made Easy

At ZeroDev, we deploy a lot of contracts.  Every release of [Kernel](https://github.com/zerodevapp/kernel) or [a plugin](https://docs.zerodev.app/use-wallets/overview) involves deploying contracts on 10+ networks, including both mainnets and testnets.  This is a super tedious process because we have to acquire gas tokens on all these networks; testnet tokens, in particular, can be hard to acquire due to faucet limits.

This issue is not unique to ZeroDev, of course.  All multi-chain Web3 projects need to tackle multi-chain deployment.  The issue is even more pronounced in larger teams, since the developer deploying contracts may not be the person with access to the company’s treasury, so a complicated reimbursement process follows each deployment, where the developer tries to figure out how much $$$ they should be reimbursed from spending 10+ tokens.

TLDR: multi-chain contract deployment has been a headache — until now.  We’ve created [Orchestra](https://github.com/zerodevapp/orchestra), a CLI for deploying contracts on multiple chains without needing tokens on each chain.  Here you can see it in action:

<p align="center">
  <img src="/img/orchestra.gif" width="100%" />
</p>

# How it works

How is Orchestra able to deploy contracts on multiple chains without requiring tokens for each chain?  You guessed it — ERC-4337 paymasters.

When you set up Orchestra, it creates a Kernel smart account owned by your private key.  This smart account is then used to deploy contracts.  Since it’s a smart account, we can sponsor gas for it using ERC-4337 paymasters, saving the account itself from having to own any tokens.

As the contract deployer, you would pay for the gas through your paymaster subscription.  For instance, if you use ZeroDev as the paymaster, you would [sign up at ZeroDev](https://dashboard.zerodev.app/) and pay with your credit card.  In other words, you can now deploy contracts on any chain with just a credit card.

# Limitations

We have successfully employed Orchestra to deploy multiple plugins, cutting the deployment time from hours to minutes.  However, the tool can still be improved:

- Orchestra currently uses only ZeroDev infra, but it can in principle work with any AA infra.  We welcome PRs to add support for other infra providers such as StackUp, Pimlico, Alchemy, etc.
- Orchestra currently only supports deterministic deployment using `CREATE2`, through the widely-used [deterministic deployment proxy](https://github.com/Arachnid/deterministic-deployment-proxy) which ensures that your contract will have the same address on every chain.  For most projects this is exactly what they want, but we welcome PRs for non-deterministic deployments.

# Get Started

[See instructions here](https://github.com/zerodevapp/orchestra) to get started!
