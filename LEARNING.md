# Over-Collateralized Lending

This challenge implements a lending market where ETH collateral backs CORN debt at a minimum 120% ratio. The protocol values collateral through the accompanying CORN/ETH DEX, blocks unsafe borrowing and withdrawals, accepts repayments, and lets a third party close an unsafe position for a 10% collateral reward.

## Core invariants

- A user cannot create or worsen a position below the 120% collateral ratio.
- Debt and collateral accounting are updated before external token or ETH transfers; a revert restores the complete transaction.
- A liquidation repays all recorded debt and cannot distribute more ETH than the borrower deposited.
- Users with no debt receive the maximum position ratio so they are never liquidatable.

## Validation

- `yarn test`: 21 passing tests.
- `yarn hardhat:compile`: successful.
- `yarn next:build`: successful with only the scaffold's existing deprecated event-history warnings.
- Sepolia deployment: `0xb83c92ccbff0101336e376377d14587849282229`.
- Public frontend: https://speedrunethereum-over-collateralize-five.vercel.app
- SpeedRunEthereum autograder: accepted with 21/21 tests; profile reached 110 XP.

The DEX is a teaching oracle and can be manipulated. Production lending systems need a robust oracle design, interest accounting, partial liquidation rules, bad-debt handling, and reentrancy protection appropriate to their asset model.
