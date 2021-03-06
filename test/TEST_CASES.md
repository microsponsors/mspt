# Test Scenarios

## Local Setup

Start ganache in one terminal locally via `$ ganache-cli -p 8545
`, then deploy and start truffle console in another.

Assumes the companion Registry smart contract is already deployed. Update its deployed address in this repo: `/migrations/2_deploy_contracts.js`.

```
$ npm run deploy
$ truffle console --network development
> Microsponsors.deployed().then(inst => { m = inst })
> admin = "<paste 1st address from ganache>"
> account1 = "<paste from ganache>"
> account2 = "<paste from ganache>"
> account3 = "<paste from ganache>"
> msptAddr = "<paste from ganache>"
> m.updateRegistryAddress("0x994e3a0eedee6413d606961a41bceb8441f32df3")
> m.registry()  # echoes out Registry contract address
> m.updateTokenURIBaseURL("https://api.microsponsors.io/")
```
The test scenarios above assume you're querying from truffle console.
`m` = instance created when you deployed this contract.

---

# Test Cases
`Admin` below refers to methods that the the `owner` of the contract (only) has access to.

## Admin
#### symbol()
#### paused()
#### pause()
#### unpause()
#### updateTokenURIBaseURL()
#### tokenURIBaseURL()

## Admin: Ownership
#### owner1()
#### transferOwnership1()
#### owner2()
#### transferOwnership2()

## Admin: Registry management
#### registry() - public read method
#### updateRegistryAddress()

## Admin: Mint Fee
#### mintFee() - public method
#### updateMintFee()
#### withdrawBalance()

## Mint
#### mint()
```javascript
// Assumes you're in Truffle console, see "Local Setup" info above.
m.mint("bdns%3Afoo.com", 1579332938665, 1579632938666, false, 1, { value: 100000000000000, from: account1 });
// --> works, if you send mintFee as msg.value
// --> should fail if Content ID is not registered to acct in Registry
//       or account is not whitelisted
// --> should fail without mintFee sent as msg.value

m.mint("bdns%3Afoo.com", 1579332938665, 1579332938660, false, 1, {value: 100000000000000, from: account1 });
// --> should fail bc startTime is after endTime
```
#### safeMint()

## Gets
#### ownerOf()
#### balanceOf()
#### tokenURI()
#### tokenTimeSlot()
#### totalSupply()
#### tokensOfOwner()
#### tokensMintedBy()
#### tokenMinterContentIds()
#### tokenFederationId()

## Transfers
#### approve()
#### getApproved()
#### setApprovalForAll()
#### isApprovedForAll()
#### transferFrom()
#### safeTransferFrom()

## Burns
#### burn()
