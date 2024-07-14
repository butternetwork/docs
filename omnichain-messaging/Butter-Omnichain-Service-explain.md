

## What is Butter Omnichain Service

It is a cross-chain messaging service composed of OmniServiceRelay on the Mapo chain and OmniService on other chains, enabling users to provide cross-chain services more securely, efficiently, and conveniently.

## How to Use

#### The source chain initiates cross-chain.

When initiating cross-chain on the source chain contract, it is necessary to introduce the IMOSV3 interface. You can directly import the protocol using the following code, but make sure to install the protocol with ```'npm install @butternetwork/omniservice``` before usage.

```
@butternetwork/omniservice/contracts/interface/IMOSV3.sol;
```

When initiating a cross-chain request, in addition to the data you wish to execute across chains, we also provide various applicable scenarios for users to flexibly choose the most suitable method according to their own needs.

```
    enum MessageType {
        CALLDATA,
        MESSAGE
    }

    struct MessageData {
        bool relay;
        MessageType msgType;
        bytes target;
        bytes payload;
        uint256 gasLimit;
        uint256 value;
    }
```

Check the structure of MessageData.

- By default, when `relay` is false, it means that during the cross-chain message passing through the relay chain (Mapo), no additional processing is done, and the message is directly sent to the target chain's event.
  - If there is a requirement to set `relay` to true, then during the cross-chain message process, when passing through the relay chain (Mapo), the `mapoExecute` method will also be executed to obtain the newly returned payload, which will then be sent to the target chain's event.
- Currently, there are two choices for `msgType`
  - `MESSAGE` allows for freely defined cross-chain messages. When they reach the target chain, the cross-chain messages are passed to the `mapoExecute` method. You can define your own preferred checking methods and data processing in this method to complete the cross-chain message execution.
  - `CALLDATA` requires the complete `calldata` to be prepared on the source chain for execution on the target. OmniService contract should be granted appropriate permissions to execute the call.
- `target` is the contract address where the message will be executed upon reaching the target chain
- `payload` is the data intended for cross-chain transmission.
- `gasLimit` is the maximum gas limit allowed for execution on the target chain.
- `value` should currently be defaulted to 0; further details will be forthcoming.

After understanding the various options available for `MessageData`, we can directly encode the assembled `MessageData` and then call `transferOut` to send the cross-chain request.

```
    bytes memory messageData = abi.encode(MessageData({}));
    
    function transferOut(
        uint256 toChain,
        bytes memory messageData,
        address feeToken
    ) external payable returns (bytes32);
```



#### The target chain executes the cross-chain message

When our message reaches the target chain, we will execute the cross-chain message according to the choice made during cross-chain initiation, and emit an event upon completion of execution. Depending on the `msgType` chosen freely during cross-chain initiation, we will employ different handling methods on the target chain.

- The `MESSAGE` mode offers greater freedom and broader adaptability, but requires users to implement the following interfaces on the target chain.

  ```
      function mapoExecute(
          uint256 _fromChain,
          uint256 _toChain,
          bytes calldata _fromAddress,
          bytes32 _orderId,
          bytes calldata _message
      ) external returns (bytes memory newMessage)
  ```

  If you want to facilitate the implementation of the `mapoExecute` method, you can directly install the `@butternetwork/omniservice` protocol and import the `IMapoExecutor` interface using the following code:

  ```
  import "@butternetwork/omniservice/contracts/interface/IMapoExecutor.sol";
  ```

  The `mapoExecute` method is flexible. We will pass the information from the source chain along with your custom message. You can freely define the validation rules, including decoding the message, among other things. This method is suitable for a wide range of scenarios.

- The `CALLDATA` mode involves preparing the calldata for execution on the target chain at the time of initiating the cross-chain request. The `OmniService` will directly execute the call and then emit an event upon completion.

Of course, we also consider that there are many different chains currently. Because data cannot perfectly intercommunicate between chains, we have created the Butter Omnichain Service to accomplish this great feat. Each chain has its own characteristics, and occasional execution failures are inevitable. But don't worry, even if cross-chain execution fails, we will save the hash of the failed execution. You can retrieve the information for re-execution through the transaction logs, allowing you to correct the execution logic and attempt the cross-chain message execution again. For more details, please see below:

```
    function retryMessageIn(
        uint256 _fromChain,
        bytes32 _orderId,
        bytes calldata _fromAddress,
        bytes calldata _messageData
    ) external 
```

`retryMessageIn` is flexible and can be called with any correct data for execution. It does not alter the cross-chain message, as we save the hash at the time of failure and will perform hash validation. It simply provides more opportunities for attempts, making cross-chain communication more free and seamless.

## Butter Omnichain Service Event 

```
	event MessageOut(
        uint256 indexed fromChain,
        uint256 indexed toChain,
        bytes32 orderId,
        bytes fromAddrss,
        bytes messageData
    );
    
    event MessageIn(
        uint256 indexed fromChain,
        uint256 indexed toChain,
        bytes32 orderId,
        bytes fromAddrss,
        bytes messageData,
        bool result,
        bytes reason
    );
```

