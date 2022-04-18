# Access Control


- In myERC20Token it is implemented a Role-Based Access Control mechanism (https://en.wikipedia.org/wiki/Role-based_access_control) using the AccessControl.sol smart contract of the OpenZeppelin library.
- A role authorizes an account to call a specific function inside the token’s smart contract. Accounts can have 0 or more roles.
- Defining roles.
    Three roles were defined in the MyTokenERC20 implementation:
    1. Burner role
    2. Minter role
    3. Pauser role

- Using roles.
Roles are saved inside the AccessControl.sol smart contract using the “_roles” mapping and the “RoleData” structure,

- In the above code, the “RoleData” structure contains a mapping between an address and a boolean value. The “_roles” member of the AccessControl smart contract is a mapping between a role and the account having that role. Given an account and a role, you can test if the account has the role by looking at the “members” field of “RoleData”.

- Checking the role of accounts to authorize operations on smart contract.

    In order to check that an account has the role to perform the specific action the require() function is used. It can be used in two ways:
    by directly calling require() inside the function body of the privileged function;
    by defining the require() statement inside a modifier and including the modifier inside the privileged function.

Note about TimeLock.
Please note that OpenZeppelin provides also a TimeLock mechanism to enforce the security policy, specifically this mecanism can be used in order to not let an administrator perform a malicious task.
For example, the timelock security mechanism can be used by legitimate projects to prevent “rug pull” scams.