# MOFH-Client

![](https://img.shields.io/npm/v/mofh-client.svg)
![npm bundle size](https://img.shields.io/bundlephobia/minzip/mofh-client.svg)

A MyOwnFreeHost client that you can use with server-side javascript.

## Install

With npm:

```sh
npm install mofh-client
```

## configure mofh-client

In a `.env` file in main directory of project enter your mofh api user and mofh api key, which you can find [here](http://panel.myownfreehost.net/panel/index2.php?option=api).

```env
mofh_api_user='your-mofh-api-user'
mofh_api_key='your-mofh-api-key'
```
You will also need to set the IP your code is running on inside the panel (linked above) to be allowed to call the MOFH API.

## Usage

### create an account on MOFH:

```javascript
const createAccount: (username: string, password: string, email: string, domain: string, plan: string) => any
```

- asynchronous

- @param username — A unique, 8 character identifier of the account.

- @param password — their password to login to the control panel, FTP and databases.

- @param email — their email.

- @param domain — their domain. Can be a subdomain or a custom domain.

- @param plan — the hosting plan to create the account on. Requires a hosting package to be configured through MyOwnFreeHost.

- @returns — json: **"success"**: whether or not you should be showing the response to the user. **"message"**: `{ "status": 1 or 0 depending on success, "statusmsg": the response of the request, "vpusername": their vistapanel username if success, }`. **"error"**: the error, if there is one

Example:
```javascript
//returns '{"success": true, "message": 1, "error": ''}'
const mofh = require('mofh-client');
console.log(mofh.createAccount('username', 'password', 'email@email.com', 'valid.domain.com', 'freeplan01'));
```

### Get a list of a user's domains:

```javascript
const getUserDomains: (username: string) => any
```

- asynchronous

- @param username — The unique, 8 character identifier of the account.

- @returns — json: **"success"**: whether or not you should be showing the response to the user. **"message"**: either be empty array (i.e. an error occured or no domains found) or contain array of websites in the form of `[["status e.g. ACTIVE", "the url"], etc.]`. **"error"**: the error, if there is one

Example:
```javascript
//returns '{"success": true, "message": [["status e.g. ACTIVE", "the url"], etc.], "error": ''}'
const mofh = require('mofh-client');
console.log(mofh.getUserDomains('validusername'));
```

### Get availability of a domain:

```javascript
const getAvailability: (domain: string) => any
```

- asynchronous

- @param domain — The domain name or subdomain to check.

- @returns — json: **"success"**: whether or not you should be showing the response to the user. **"message"**: either be 0 (not available/failed to check) or 1 (available+succeeded). **"error"**: the error, if there is one

Example:
```javascript
//returns '{"success": true, "message": 1, "error": ''}'
const mofh = require('mofh-client');
console.log(mofh.getUserDomains('valid.domain.com'));
```

### Reset a User's Password:

```javascript
const resetPassword: (username: string, password: string) => any
```

- asynchronous

- @param username — The unique, 8 character identifier of the account.

- @param password — their new password

- @returns — json: **"success"**: whether or not you should be showing the response to the user. **"message"**: `{ "status": 1 or 0 depending on success, "statusmsg": 'Success' or error containing response and letter x for suspended, r for reactivating, and c for closing,}`. **"error"**: the error, if there is one

Example:
```javascript
//returns '{"success": true, "message": 1, "error": ''}'
const mofh = require('mofh-client');
console.log(mofh.resetPassword('username', 'newpassword'));
```

### Suspend an Account:

```javascript
const suspendAccount: (username: string, reason: string) => any
```

- asynchronous

- @param username — The unique, 8 character identifier of the account.

- @param reason — Information about why you are suspending the account. at least 5 chars long.

- @returns — json: **"success"**: whether or not you should be showing the response to the user. **"message"**: `{ "status": 1 or 0 depending on success, "statusmsg": non existant if success, error response if fail}`. **"error"**: the error, if there is one

Example:
```javascript
//returns '{"success": true, "message": 1, "error": ''}'
const mofh = require('mofh-client');
console.log(mofh.suspendAccount('username', 'innapropriate content'));
```

### Unsuspend an Account:

```javascript
const unsuspendAccount: (username: string) => any
```

- asynchronous

- @param username — The unique, 8 character identifier of the account.

- @returns — json: **"success"**: whether or not you should be showing the response to the user. **"message"**: `{ "status": 1 or 0 depending on success, "statusmsg": non existant if success, error response if fail}`. **"error"**: the error, if there is one

Example:
```javascript
//returns '{"success": true, "message": 1, "error": ''}'
const mofh = require('mofh-client');
console.log(mofh.suspendAccount('username', 'innapropriate content'));
```

## License

Licensed under the MIT License