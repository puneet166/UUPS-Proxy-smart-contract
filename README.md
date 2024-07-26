# UUPS-Proxy-smart-contract
This repo contain UUPS bases proxies smart contracts for learning purpose


# Smart Contract Deployment and Upgrade Guide

This guide details the steps required to deploy and upgrade a smart contract using a proxy pattern.

## Steps

### Step 1: Deploy the Implementation Smart Contract

1. Deploy the implementation smart contract.
2. Save the address of the deployed implementation smart contract for further use.

### Step 2: Deploy the Proxy Smart Contract

1. Deploy the `proxy.sol` smart contract with the following parameters:
    - **constructData**: The function name and parameters encoded in byte form. Use [https://abi.hashex.org/](https://abi.hashex.org/) to encode this data.This "constructData" is the function which intialte the implementation smart contract.
    - **Implementation Address**: The address of the deployed implementation smart contract.

### Step 3: Delegation Call via Proxy Smart Contract

1. After successfully deploying both the proxy and implementation v1 smart contracts, perform a delegation call to the target smart contract through the proxy.
2. To perform the delegation call:
    - Encode the target contract's (implementation smart contract) function that you want to call from the proxy using [https://abi.hashex.org/](https://abi.hashex.org/).
    - Pass the encoded data into the delegate Low level interactions calldata in remix through the proxy.
3. Once the function of the implementation smart contract is called, read the updated status through the proxy:
    - Use the proxy smart contract address and the implementation smart contract ABI to get the updated proxy values. This call will happend through the web3 node.js.

### Step 4: Upgrade the Implementation Smart Contract

1. Deploy the newly implemented V2 smart contract.

### Step 5: Update the Proxy to Use V2

1. Call the V1 smart contract function `updateCode(address newCode)` with the new code (V2 smart contract address):
    - First, encode the function with the parameter using [https://abi.hashex.org/](https://abi.hashex.org/).
    - Pass the encoded data in the delegate call,  Low level interactions calldata in remix thrugh the proxy.

### Step 6: Verify Upgrade

1. Once the update is complete, verify that the proxy is now mapped to V2. for verification do the follow step 3.

## Important Notes

- Ensure implementation v1 smart contracts have the same number of variables, and maintain the same variable order in the upgradable v2 smart contract.
- You can add more variables in the new implementation smart contract v2, but do not remove older variables from the previous contract v1 variables .


FOr more details visit here - https://www.youtube.com/watch?v=bPOOvyVpI9U and https://coinsbench.com/creating-an-ethereum-solidity-proxy-contract-using-remix-b9dda8b9a3a2

