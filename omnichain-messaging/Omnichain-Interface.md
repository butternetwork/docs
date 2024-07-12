# OmniService Interface

OmniService on EVM

## initialize

perform initialization

### Function

function initialize(address _owner) public 

### Parameters

| parameter | type    | comment                        |
| --------- | ------- | ------------------------------ |
| _owner    | address | This is contract owner address |

## transferOut

OmniService transfer out of message data

### function

```
function transferOut(
    uint256 _toChain,
    bytes memory _messageData,
    address _feeToken
) external payable virtual returns (bytes32);
```

### parameters

| parameter    | type    | comment                                                      |
| ------------ | ------- | ------------------------------------------------------------ |
| _toChain     | uint256 | Target chain id to transfer out                              |
| _messageData | bytes   | This is the information encoded from `MessageData`           |
| _feeToken    | address | This is the address of the token you want to use to pay the fee |

### Return Value

| type    | comment                                 |
| ------- | --------------------------------------- |
| bytes32 | The order ID of the cross-chain message |

## messageOut

OnmiService sends a cross-chain message

### Function

```
function messageOut(
	bytes32 _transferId,
	address _initiator,
	address _referrer,
	uint256 _toChain,    
	bytes memory _messageData,    
	address _feeToken
) external payable virtual returns (bytes32);
```

### Parameters

| parameter    | type    | comment                                                      |
| ------------ | ------- | ------------------------------------------------------------ |
| _transferId  | bytes32 | Custom identifier provided by the caller                     |
| _initiator   | address | The actual address of the message initiator, which is typically a user address |
| _referrer    | address | Custom parameter provided by the caller, which can serve as an identifier for the caller |
| _toChain     | uint256 | The chain id of the target chain                             |
| _messageData | bytes   | This is the information encoded from `MessageData`           |
| _feeToken    | address | This is the address of the token you want to use to pay the fee |

### Return Value

| type    | comment                                 |
| ------- | --------------------------------------- |
| bytes32 | The order ID of the cross-chain message |

## transferInWithIndex

After `messager` scans and detects the cross-chain log, validation on the target chain is completed, thus finalizing the cross-chain message.

### Function

```
function transferInWithIndex(
    uint256 _chainId,
    uint256 _logIndex,
    bytes memory _receiptProof
) external;
```

### Parameters

| parameter     | type    | comment                                                   |
| ------------- | ------- | --------------------------------------------------------- |
| _chainId      | uint256 | The chain ID of the source chain                          |
| _logIndex     | uint256 | The index of the cross-chain log in the transaction logs. |
| _receiptProof | bytes   | Merkle proof validated through a light node.              |

## transferInVerify

After `messager` scans and detects the cross-chain log, validation is completed on the target chain.

### Function

```
function transferInVerify(
    uint256 _chainId,
    uint256 _logIndex,
    bytes memory _receiptProof
) external
```

### Parameters

| parameter     | type    | comment                                                   |
| ------------- | ------- | --------------------------------------------------------- |
| _chainId      | uint256 | The chain ID of the source chain                          |
| _logIndex     | uint256 | The index of the cross-chain log in the transaction logs. |
| _receiptProof | bytes   | Merkle proof validated through a light node.              |

## transferInVerified

After the message is validated, the cross-chain message is completed.

### Function

```
function transferInVerified(
    bytes32 _orderId,
    uint256 _fromChain,
    bytes calldata _fromAddress,
    bytes calldata _messageData
) external;
```

### Parameters

| parameter    | type    | comment                                                 |
| ------------ | ------- | ------------------------------------------------------- |
| _orderId     | bytes32 | The order ID of the cross-chain message                 |
| _fromChain   | uint256 | The chain ID of the source chain                        |
| _fromAddress | bytes   | The address of the source chain                         |
| _messageData | bytes   | This is the `messageData` validated by the source chain |

## retryMessageIn

When a message execution fails, the contract stores the hash of the relevant information. Passing the corresponding parameters allows for retrying the execution of the cross-chain message.

### Function

```
function retryMessageIn(
    uint256 _fromChain,
    bytes32 _orderId,
    bytes calldata _fromAddress,
    bytes calldata _messageData
) external;
```

### Parameters

| parameter    | type    | comment                                                 |
| ------------ | ------- | ------------------------------------------------------- |
| _orderId     | bytes32 | The order ID of the cross-chain message                 |
| _fromChain   | uint256 | The chain ID of the source chain                        |
| _fromAddress | bytes   | The address of the source chain                         |
| _messageData | bytes   | This is the `messageData` validated by the source chain |

## addRemoteCaller

Granting the source chain the chain ID and address permissions to execute messages.

### Function

```
function addRemoteCaller(uint256 _fromChain, bytes memory _fromAddress, bool _tag) external;
```

### Parameters

| parameter    | type    | comment                                                      |
| ------------ | ------- | ------------------------------------------------------------ |
| _fromChain   | uint256 | The chain ID of the source chain                             |
| _fromAddress | bytes   | The address of the source chain                              |
| _tag         | bool    | True indicates permission granted, false indicates permission not granted |



## getMessageFee

Get the specific fee for the target chain.

### Function

```
function getMessageFee(    
	uint256 _toChain,    
	address _feeToken,    
	uint256 _gasLimit
) external view returns(uint256 amount, address receiverAddress);
```

### Parameters

| parameter | type    | comment                                                      |
| --------- | ------- | ------------------------------------------------------------ |
| _toChain  | uint256 | The chain id of the target chain                             |
| _feeToken | address | This is the address of the token you want to use to pay the fee |
| _gasLimit | uint256 | Customizable gas limit                                       |

### Return Value

| value           | type    | comment                            |
| --------------- | ------- | ---------------------------------- |
| amoun           | uint256 | The amount of the fee              |
| receiverAddress | address | The address that receives the fee. |



## getExecutePermission

To check if the source chain's chain ID and address have permission to execute cross-chain messages on the target chain:

- True means permission is granted (可以执行).
- False means permission is not granted (不行).

### Function

```
function getExecutePermission(    
	address _targetAddress,    
	uint256 _fromChain,    
	bytes memory _fromAddress
) external view override returns (bool)
```

### Parameters

| parameter      | type    | comment                                  |
| -------------- | ------- | ---------------------------------------- |
| _targetAddress | address | The contract address on the target chain |
| _fromChain     | uint256 | The chain id of the target chain         |
| _fromAddress   | bytes   | The address of the source chain          |

### Return Value

| type | comment                                                      |
| ---- | ------------------------------------------------------------ |
| bool | True indicates permission granted, false indicates permission not granted. |

