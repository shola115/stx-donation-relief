# STX Donation Relief Smart Contract

## Overview
This smart contract facilitates a disaster relief donation system where users can donate funds, administrators can manage recipients and contract settings, and recipients can withdraw allocated funds. The contract includes robust security measures such as withdrawal cooldowns, admin controls, and an emergency shutdown feature.

## Features
- **Donations**: Users can donate funds to the relief pool.
- **Recipient Management**: Administrators can add, update, or remove recipients.
- **Fund Withdrawals**: Recipients can withdraw allocated funds subject to a cooldown period.
- **Admin Controls**: Admins can set donation limits, update contract settings, and pause contract functions.
- **Emergency Shutdown**: The admin can halt all operations in case of a security risk.
- **Refund Requests**: Donors can request refunds within a specified period.

## Constants
- **ERR_UNAUTHORIZED (u1)**: Unauthorized action error.
- **ERR_INVALID_AMOUNT (u2)**: Invalid donation or withdrawal amount error.
- **ERR_INSUFFICIENT_FUNDS (u3)**: Insufficient contract funds error.
- **ERR_RECIPIENT_NOT_FOUND (u4)**: Attempting to interact with a non-existent recipient.
- **ERR_RECIPIENT_EXISTS (u5)**: Trying to add an already existing recipient.
- **ERR_NOT_CONFIRMED (u8)**: Confirmation missing for recipient removal.
- **ERR_UNCHANGED_STATE (u9)**: No change detected in contract state.
- **Withdrawal Cooldown**: 24 hours (u86400 seconds) between withdrawals.

## Data Structures
### Variables
- **total-funds (uint)**: Tracks the total amount of funds in the contract.
- **admin (principal)**: Stores the admin's principal.
- **min-donation (uint)**: Minimum donation amount allowed.
- **max-donation (uint)**: Maximum donation amount allowed.
- **paused (bool)**: Indicates whether the contract is paused.

### Maps
- **donations (principal → uint)**: Stores donation amounts per donor.
- **recipients (principal → uint)**: Stores recipient allocations.
- **last-withdrawal (principal → uint)**: Stores the last withdrawal timestamp for each recipient.

## Functions

### Public Functions
#### `donate (amount uint) → (response uint)`
Allows users to donate funds, provided the contract is active and the amount is within limits.

#### `add-recipient (recipient principal, allocation uint) → (response tuple)`
Allows the admin to add a new recipient with a specified allocation.

#### `withdraw (amount uint) → (response bool)`
Allows recipients to withdraw funds, subject to allocation and cooldown restrictions.

#### `set-admin (new-admin principal) → (response principal)`
Allows the current admin to assign a new admin.

#### `set-donation-limits (new-min uint, new-max uint) → (response bool)`
Allows the admin to set minimum and maximum donation amounts.

#### `set-paused (new-paused-state bool) → (response bool)`
Allows the admin to pause/unpause contract operations.

#### `update-recipient-allocation (recipient principal, new-allocation uint) → (response bool)`
Allows the admin to update a recipient's allocated funds.

#### `remove-recipient (recipient principal) → (response bool)`
Allows the admin to remove a recipient from the list.

#### `confirm-remove-recipient (recipient principal, confirm bool) → (response bool)`
Requires admin confirmation before removing a recipient.

#### `request-refund (amount uint) → (response bool)`
Allows donors to request a refund within the allowed period.

#### `emergency-shutdown () → (response bool)`
Enables the admin to halt all operations in emergency situations.

#### `log-audit (action-type string, actor principal) → (response bool)`
Logs administrative actions for auditing purposes.

### Read-Only Functions
#### `get-donation (user principal) → (uint)`
Returns the total donations made by a specific user.

#### `get-total-funds () → (uint)`
Returns the total funds available in the contract.

#### `is-paused () → (bool)`
Returns whether the contract is currently paused.

#### `get-recipient-allocation (recipient principal) → (uint)`
Returns the allocated funds for a specific recipient.

#### `get-admin () → (principal)`
Returns the current admin's principal.

#### `get-user-history (user principal) → (tuple)`
Returns a user’s donation and withdrawal history.

## Security Measures
- **Admin Controls**: Only the admin can modify recipients, contract settings, and trigger shutdowns.
- **Cooldown Periods**: Prevents abuse of frequent withdrawals and refunds.
- **Error Handling**: Uses predefined error codes for security and debugging.
- **Emergency Shutdown**: Allows the admin to halt all operations during an emergency.

## Deployment & Usage
1. Deploy the contract on the Stacks blockchain.
2. The deploying account becomes the initial admin.
3. Users can donate using the `donate` function.
4. The admin manages recipients and allocations.
5. Recipients withdraw funds as needed, following cooldown restrictions.
6. The admin can adjust settings, pause the contract, or perform an emergency shutdown.

## Future Enhancements
- Implement a multi-admin system for added security.
- Introduce dynamic allocation adjustments based on recipient needs.
- Enable automated fund distribution to recipients at scheduled intervals.

## License
This smart contract is licensed under the MIT License.

