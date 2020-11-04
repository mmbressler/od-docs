# Geb

The main package used to interact with the core GEB contracts.

## Constructors

+ **new Geb**\(`network`: GebDeployment, `provider`: GebProviderInterface \| Provider\): [_Geb_](https://github.com/reflexer-labs/geb-docs/tree/b9a3c823f6c8a5dbc65fb8c9a9125c6d561aa46a/geb-js/geb.md)

_Defined in_ [_packages/geb/src/geb.ts:52_](https://github.com/reflexer-labs/geb.js/blob/8c78ffc/packages/geb/src/geb.ts#L52)

**Parameters:**

| Name | Type | Description |
| :--- | :--- | :--- |
| `network` | GebDeployment | Either `'kovan'`, `'mainnet'` or an actual list of contract addresses. |
| `provider` | GebProviderInterface \| Provider | Either a Ethers.js provider or a Geb provider \(Soon support for Web3 will be added\) |

**Returns:** [_Geb_](https://github.com/reflexer-labs/geb-docs/tree/b9a3c823f6c8a5dbc65fb8c9a9125c6d561aa46a/geb-js/geb.md)

## Properties

### contracts

• **contracts**: _ContractApis_

_Defined in_ [_packages/geb/src/geb.ts:50_](https://github.com/reflexer-labs/geb.js/blob/8c78ffc/packages/geb/src/geb.ts#L50)

Object containing all GEB core contracts instances for low level interactions. All contracts object offer a one-to-one typed API to the underlying smart-contract. Currently has the following contracts:

* SAFEEngine
* AccountingEngine
* TaxCollector
* LiquidationEngine
* OracleRelayer
* GlobalSettlement
* DebtAuctionHouse
* PreSettlementSurplusAuctionHouse
* PostSettlementSurplusAuctionHouse
* SettlementSurplusAuctioneer
* GebSafeManager
* GetSafes
* BasicCollateralJoin
* CoinJoin
* Coin \(RAI ERC20 contract\)
* GebProxyRegistry
* FixedDiscountCollateralAuctionHouse \(For ETH-A\)
* Weth \(ERC20\)

## Methods

### deployProxy

▸ **deployProxy**\(\): _TransactionRequest_

_Defined in_ [_packages/geb/src/geb.ts:113_](https://github.com/reflexer-labs/geb.js/blob/8c78ffc/packages/geb/src/geb.ts#L113)

Deploy a new proxy owned by the sender.

**Returns:** _TransactionRequest_

### getErc20Contract

▸ **getErc20Contract**\(`tokenAddress`: string\): _Erc20_

_Defined in_ [_packages/geb/src/geb.ts:241_](https://github.com/reflexer-labs/geb.js/blob/8c78ffc/packages/geb/src/geb.ts#L241)

Returns an object that can be used to interact with a ERC20 token. Example:

```typescript
const USDCAddress = "0xa0b86991c6218b36c1d19d4a2e9eb0ce3606eb48"
const USDC = geb.getErc20Contract(USDCAddress)

// Get 0xdefiisawesome's balance
const balance = USDC.balanceOf("0xdefiisawesome..")

// Send 1 USDC to 0xdefiisawesome (USDC is 6 decimals)
const tx = USDC.transfer("0xdefiisawesome..", "1000000")
await wallet.sendTransaction(tx)
```

**Parameters:**

| Name | Type | Description |
| :--- | :--- | :--- |
| `tokenAddress` | string | Token contract address |

**Returns:** _Erc20_

Erc20

### getGebContract

▸ **getGebContract**‹**T**›\(`gebContractClass`: GebContractAPIConstructorInterface‹T›, `address`: string\): _T_

_Defined in_ [_packages/geb/src/geb.ts:348_](https://github.com/reflexer-labs/geb.js/blob/8c78ffc/packages/geb/src/geb.ts#L348)

Returns an instance of a specific geb contract given a Geb contract API class at a specified address

```typescript
import { contracts } from "geb.js"
const safeEngine = geb.getGebContract(contracts.SafeEngine, "0xabcd123..")
const globalDebt = safeEngine.globalDebt()
```

**Type parameters:**

▪ **T**: _BaseContractAPI_

**Parameters:**

| Name | Type | Description |
| :--- | :--- | :--- |
| `gebContractClass` | GebContractAPIConstructorInterface‹T› | Class from contracts or adminContracts |
| `address` | string | Contract address of the instance |

**Returns:** _T_

### getProxyAction

▸ **getProxyAction**\(`ownerAddress`: string\): _Promise‹_[_GebProxyActions_](https://github.com/reflexer-labs/geb-docs/tree/b9a3c823f6c8a5dbc65fb8c9a9125c6d561aa46a/geb-js/gebproxyactions.md)_‹››_

_Defined in_ [_packages/geb/src/geb.ts:83_](https://github.com/reflexer-labs/geb.js/blob/8c78ffc/packages/geb/src/geb.ts#L83)

Given an address returns a GebProxyActions object to execute bundled operations. Important: This requires the address to have deployed a GEB proxy through the proxy registry contract. It will throw a `DOES_NOT_OWN_HAVE_PROXY` error if the address specified does not have a proxy. Use the [deployProxy](https://github.com/reflexer-labs/geb-docs/tree/b9a3c823f6c8a5dbc65fb8c9a9125c6d561aa46a/geb-js/geb.md#deployproxy) function to get a new proxy.

**Parameters:**

| Name | Type | Description |
| :--- | :--- | :--- |
| `ownerAddress` | string | Externally owned user account, Ethereum address that owns a GEB proxy. |

**Returns:** _Promise‹_[_GebProxyActions_](https://github.com/reflexer-labs/geb-docs/tree/b9a3c823f6c8a5dbc65fb8c9a9125c6d561aa46a/geb-js/gebproxyactions.md)_‹››_

### getProxyActionGlobalSettlement

▸ **getProxyActionGlobalSettlement**\(`ownerAddress`: string\): _Promise‹_[_GebProxyActionsGlobalSettlement_](https://github.com/reflexer-labs/geb-docs/tree/b9a3c823f6c8a5dbc65fb8c9a9125c6d561aa46a/geb-js/gebproxyactionsglobalsettlement.md)_‹››_

_Defined in_ [_packages/geb/src/geb.ts:97_](https://github.com/reflexer-labs/geb.js/blob/8c78ffc/packages/geb/src/geb.ts#L97)

Given an address returns a GebProxyActionsGlobalSettlement object to execute bundled operations during GlobalSettlement. **IMPORTANT**: Same as for `getProxyAction` you will need to deploy a proxy beforehand using the proxy registry.

**Parameters:**

| Name | Type | Description |
| :--- | :--- | :--- |
| `ownerAddress` | string | Externally owned user account, Ethereum address that owns a GEB proxy. |

**Returns:** _Promise‹_[_GebProxyActionsGlobalSettlement_](https://github.com/reflexer-labs/geb-docs/tree/b9a3c823f6c8a5dbc65fb8c9a9125c6d561aa46a/geb-js/gebproxyactionsglobalsettlement.md)_‹››_

### getSafe

▸ **getSafe**\(`idOrHandler`: string \| number, `collateralType?`: string\): _Promise‹_[_Safe_](https://github.com/reflexer-labs/geb-docs/tree/b9a3c823f6c8a5dbc65fb8c9a9125c6d561aa46a/geb-js/safe.md)_›_

_Defined in_ [_packages/geb/src/geb.ts:121_](https://github.com/reflexer-labs/geb.js/blob/8c78ffc/packages/geb/src/geb.ts#L121)

Get the SAFE object given a `safeManager` id or a `safeEngine` handler address.

**Parameters:**

| Name | Type | Description |
| :--- | :--- | :--- |
| `idOrHandler` | string \| number | Safe Id or SAFE handler |
| `collateralType?` | string | - |

**Returns:** _Promise‹_[_Safe_](https://github.com/reflexer-labs/geb-docs/tree/b9a3c823f6c8a5dbc65fb8c9a9125c6d561aa46a/geb-js/safe.md)_›_

### getSafeFromOwner

▸ **getSafeFromOwner**\(`address`: string\): _Promise‹_[_Safe_](https://github.com/reflexer-labs/geb-docs/tree/b9a3c823f6c8a5dbc65fb8c9a9125c6d561aa46a/geb-js/safe.md)_\[\]›_

_Defined in_ [_packages/geb/src/geb.ts:204_](https://github.com/reflexer-labs/geb.js/blob/8c78ffc/packages/geb/src/geb.ts#L204)

Fetch the list of safes owned by an address. This function will fetch safes owned directly through the safeManager and safes owned through the safe manager through a proxy. Safes owned directly by the address at the safeEngine level won't appear here.

Note that this function will make a lot of network calls and is therefore very slow. For front-ends we recommend using pre-indexed data such as the geb-subgraph.

**Parameters:**

| Name | Type | Description |
| :--- | :--- | :--- |
| `address` | string |  |

**Returns:** _Promise‹_[_Safe_](https://github.com/reflexer-labs/geb-docs/tree/b9a3c823f6c8a5dbc65fb8c9a9125c6d561aa46a/geb-js/safe.md)_\[\]›_

### multiCall

▸ **multiCall**‹**O1**, **O2**, **O3**›\(`calls`: \[MulticallRequest‹O1›, MulticallRequest‹O2›, MulticallRequest‹O3›\]\): _Promise‹\[O1, O2, O3\]›_

_Defined in_ [_packages/geb/src/geb.ts:254_](https://github.com/reflexer-labs/geb.js/blob/8c78ffc/packages/geb/src/geb.ts#L254)

Bundles several read only GEB contract call into 1 RPC single request. Useful for front-ends or apps that need to fetch many parameters from the contracts but want to minimize the network request and the load on the underlying Ethereum node. The function takes as input an Array of GEB view contract calls. **IMPORTANT**: You have to set the `multicall` parameter of the contract function to `true`, it is the always the last parameter of the function. Multicall works for all contracts in the `Geb.contracts` and can be use with any contract that inherit the `BaseContractApi`. Note that it does not support non-view calls \(Calls that require to pay gas and change the state of the blockchain\).

Example:

```typescript
import { ethers } from "ethers"
import { Geb } from "geb.js"

const provider = new ethers.providers.JsonRpcProvider("http://kovan.infura.io/...")
const geb = new Geb("kovan", provider);

const [ globalDebt, collateralInfo ] = await geb.multiCall([
    geb.contracts.safeEngine.globalDebt(true), // !! Note the last parameter set to true.
    geb.contracts.safeEngine.collateralTypes(ETH_A, true),
])

console.log(`Current global debt: ${globalDebt.toString()}`)
console.log(`Current ETH_A debt: ${collateralInfo.debtAmount}`)
```

**Type parameters:**

▪ **O1**

▪ **O2**

▪ **O3**

**Parameters:**

| Name | Type | Description |
| :--- | :--- | :--- |
| `calls` | \[MulticallRequest‹O1›, MulticallRequest‹O2›, MulticallRequest‹O3›\] | Call a read only GEB contract function. The GEB contract object needs to be called with the parameter `multicall` set to `true` as seen in the example above. |

**Returns:** _Promise‹\[O1, O2, O3\]›_

Promise Array with the result from their respective requests.

### `Static` getGebContract

▸ **getGebContract**‹**T**›\(`gebContractClass`: GebContractAPIConstructorInterface‹T›, `address`: string, `provider`: GebProviderInterface \| Provider\): _T_

_Defined in_ [_packages/geb/src/geb.ts:316_](https://github.com/reflexer-labs/geb.js/blob/8c78ffc/packages/geb/src/geb.ts#L316)

Returns an instance of a specific geb contract given Geb contract API class constructor at a specified address

**Type parameters:**

▪ **T**: _BaseContractAPI_

**Parameters:**

| Name | Type | Description |
| :--- | :--- | :--- |
| `gebContractClass` | GebContractAPIConstructorInterface‹T› | Class from contracts or adminContracts |
| `address` | string | Contract address of the instance |
| `provider` | GebProviderInterface \| Provider | Either a Ethers.js provider or a Geb provider |

**Returns:** _T_
