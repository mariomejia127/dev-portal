---
id: staking-delegator-operations
title: Delegator operations
keywords: 
- staking
- ssn
- smart contract
- zilliqa	
- delegator
- delegation
description: Delegator operations
---
---

The operations available to delegator on the smart contract are as follows
1.  Delegate stake 
2.  Withdraw Stake rewards
3.  Withdraw stake amount
4.  Complete withdrawal
5.  Stake amount redelegation

## Delegate Stake
__Description__  
`DelegateStake` accepts $ZIL deposit and delegate stake to the SSN identified by `ssnaddr`. 

:::info
Due to the non-custodial nature of phase 1 staking program, only the owner of the wallet will be able to withdraw stake amount and stake reward. The SSN operator will not have access to user's fund. 
:::

__Parameters__

`_amount`: stake amount to be deposit into the smart contract  
`ssnaddr`: the SSN to delegate to

__Transition__
```
transition DelegateStake(ssnaddr: ByStr20) 
```

__Sample Code__

| Language | Link to sample code |
| -------- | ------------------- |
| NodeJS   | coming soon |
| Java     | coming soon |
| Golang   | coming soon |

TODO: Add how to get list of SSN and corresponidng SSN addr

## Withdraw stake rewards
__Description__  
`WithdrawStakeRewards` withdraws delegator's stake rewards ($ZIL and gZIL) from a SSN.

:::info
If the delegator delegates to multiple SSN and wish to withdraw all rewwards from SSN, the user will need to call this transition multiple times, specifying different SSN address each time.
:::

__Parameters__
`ssn_operator`: The address of the SSN from which the delegator wish to withdraw reward form

__Transition__
```
transition WithdrawStakeRewards(ssn_operator: ByStr20)
```

__Sample Code__

| Language | Link to sample code |
| -------- | ------------------- |
| NodeJS   | coming soon |
| Java     | coming soon |
| Golang   | coming soon |

## Withdraw Stake Amount
__Description__  
`WithdrawStakeAmt` is the first of two operations to withdraws delegator's stake amount from a SSN. Upon successful calling of this transition, the withdrawn stake amount will enter an `unbounding` state. The delegator will need to wait for 24,000 blocks (~2 weeks) before the delegator can successfully invoke `CompleteWithdrawal` transition to complete the withdrawl back to the delegator's wallet. When the stake amount is in unbonding state, it will not be eligible for any new rewards ($ZIL or gZIL).

:::info
If the delegator delegates to multiple SSN and wish to withdraw all rewwards from SSN, the user will need to call this transition multiple times, specifying different SSN address each time.
:::

__Parameters__
`ssn`: The address of the SSN from which the delegator wish to withdraw reward form
`amt`: The amount of stake amount to withdraw from the delegation to a particular ssn

__Transition__
```
 WithdrawStakeAmt(ssn: ByStr20, amt: Uint128)
 ```

__Sample Code__

| Language | Link to sample code |
| -------- | ------------------- |
| NodeJS   | coming soon |
| Java     | coming soon |
| Golang   | coming soon |


## Complete Withdrawal
__Description__
`CompleteWithdrawal` is the second of two operations required for withdrawal of delegator's stake amount from a SSN, The delegator's will first need to invoke `WithdrawStakeAmt` transition successfully, wait for 24,000 blocks (~2 weeks) for unbonding of stake amount to be over, and finally call `CompleteWithdrawal` in a seperate transaction to complete the withdrawal and receive the stake amount back into the delegator's wallet.

`CompleteWithdrawal` will iterate through all stake amount that has transitted to `unbonding` state, identify amount that have completed the unbonding process and withdraw it back to delegator's wallet. This operation is agnostic to SSN. 

__Parameters__  
None

__Transition__
```
 CompleteWithdrawal()
 ```

__Sample code__

| Language | Link to sample code |
| -------- | ------------------- |
| NodeJS   | coming soon |
| Java     | coming soon |
| Golang   | coming soon |


## Stake Amount Redelegation
__Description__
`ReDelegateStake` allows delegator to transfer stake amount from one SSN to another SSN. The stake amount will not enter unbonding state, however, buffering of stake amount may still applies.

__Parameters__  
`ssnaddr`: the existing SSN where the stake amount will be withdraw and transfer to the new SSN
`to_ssn`: the new SSN to accept the stake amount delegation
`amt`: the amount of the stake amount to transfer to the new SNN

__Transition__
```
transition ReDelegateStake(ssnaddr: ByStr20, to_ssn: ByStr20, amt: Uint128)
```

__Sample Code__

| Language | Link to sample code |
| -------- | ------------------- |
| NodeJS   | coming soon |
| Java     | coming soon |
| Golang   | coming soon |