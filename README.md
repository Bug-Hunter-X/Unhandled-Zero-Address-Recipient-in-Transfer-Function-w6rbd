# Unhandled Zero Address Recipient in Transfer Function

This Solidity code demonstrates an uncommon error:  an unhandled exception when transferring tokens to the zero address (0x0000000000000000000000000000000000000000).  While the `require` statement checks for sufficient balance, it doesn't handle the case where the recipient is invalid.

The `bug.sol` file contains the vulnerable code. The `bugSolution.sol` file presents a corrected version.

## Vulnerability

Sending tokens to the zero address will cause the transaction to fail silently in this example (it would revert in a more robust implementation), but can expose your contract to attacks if not handled carefully.  In some edge cases (e.g. using an older solidity compiler version), the transaction may unexpectedly succeed but with the token going to an invalid address.

## Solution

The solution involves adding an additional `require` statement to check if the recipient address is not the zero address before proceeding with the transfer.

## How to Reproduce

1. Compile `bug.sol`.
2. Deploy the contract.
3. Attempt to transfer tokens to the zero address (0x0000000000000000000000000000000000000000).

Observe that the transaction may either fail or unexpectedly succeed without reverting. 