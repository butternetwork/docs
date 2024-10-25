## Message And Relay

Example Requirement: There is a key on source chain A. As it passes through the relay chain, the corresponding value of the key on the relay chain is transmitted to chain B for storage, so that chain B can also retrieve the value corresponding to the key.

Necessary Conditions:

1. On the source chain, the Omni service interface and contract address are required to initiate a cross-chain event.
2. On the relay chain, there needs to be a relay contract that implements the `mapoExecute` method and returns standard encoded `MessageData` for cross-chain transmission.
3. On the target chain, the `IMapoExecutor` interface must be introduced to implement the `mapoExecute` method.

We initiate a cross-chain event on source chain A.

```
"@butternetwork/omniservice/contracts/interface/IMOSV3.sol";

contract A {
    //The contract address of OmniService on chain A
    IMOSV3 public imosv3;
    
   	function sendDictionaryMessage(
        uint256 _tochainId, //The chain ID of the target chain.
        bytes memory _target, //The contract address on the target chain.
        string memory _key //The message key on chain A.
    ) external payable {
    	//Encode the message that needs to be cross-chain.
        bytes memory data = abi.encode(_key);
		
        IMOSV3.MessageData memory mData = IMOSV3.MessageData(
            //It means that cross-chain transactions will undergo processing on the relay chain 
            //and then proceed with the cross-chain operation.
            true,
            IMOSV3.MessageType.MESSAGE,
            //When relay is true, you need to use the target address on the relay chain.
            _target, 
            data,
            500000,
            0
        );
		
        //Encode the MessageData structure for cross-chain transmission.
        bytes memory mDataBytes = abi.encode(mData);
        
        //Retrieve the amount of fee required for cross-chain transaction.
        (uint256 amount, ) = imosv3.getMessageFee(_tochainId, address(0), 500000);
        
        //Initiate the cross-chain request using OmniChain Service
        imosv3.transferOut{value: amount}(_tochainId, mDataBytes, address(0));
    }
}
```

After `messager` detects the cross-chain log, it processes the cross-chain message on the relay chain, then continues to send the `newMessage` received to initiate a cross-chain event on the target chain.

```
"@butternetwork/omniservice/contracts/interface/IMOSV3.sol";
import "@butternetwork/omniservice/contracts/interface/IMapoExecutor.sol";

contract RelayChain is IMapoExecutor {
    mapping(string => string) public dictionaryList;
    mapping(uint256 => bytes) public targetList;
    
    function mapoExecute(
        uint256 _fromChain,
        uint256 _toChain,
        bytes calldata _fromAddress,
        bytes32 _orderId,
        bytes calldata _message
    ) external override returns (bytes memory newMessage) {
		
        (string memory key) = abi.decode(_message, (string));
        
        bytes memory data = abi.encode(key,dictionaryList[key]);
        
        IMOSV3.MessageData memory mData = IMOSV3.MessageData(
            true, 
            IMOSV3.MessageType.MESSAGE, //Select MESSAGE for cross-chain transmission.
            targetList[_toChain], 
            data,
            500000,
            0
        );
		
        //Encode the MessageData structure for cross-chain transmission.
        newMessage = abi.encode(mData);
		
        return newMessage;
    }
    
}
```

We implement `mapoExecute` on chain B to finalize the cross-chain message execution.

```
import "@butternetwork/omniservice/contracts/interface/IMapoExecutor.sol";

contract B is IMapoExecutor {
	mapping(bytes32 => bool) orderList;
	//In a simple example, here's a mapping used to store cross-chain data 
	//(this can be any other type, this is just a simple example)
	mapping(string => string) public dictionary;
	
  	function mapoExecute(
        uint256 _fromChain,
        uint256 _toChain,
        bytes calldata _fromAddress,
        bytes32 _orderId,
        bytes calldata _message
    ) external override returns (bytes memory newMessage) {
        //On the target chain,
        //we can check if the orderId has been used by the source chain's chain ID (_fromChain),
        //the target chain's chain ID (_toChain),the source chain contract address (_fromAddress), 
        //even customizing some content within the message (_message) for inspection. 
        //Here's a simple example to check if orderId has been used
        require(!orderList[_orderId],"The order id already exists");
        
        //Parse the cross-chain data to obtain the corresponding value.
        (string memory key, string memory val) = abi.decode(_message, (string, string));
        
        //Assign the data correctly to complete the cross-chain message execution.
        dictionary[key] = val;
        
        //Confirm that the order ID has been used.
        orderList[_orderId] = true;
		
        return newMessage;
    }
}
```

Advantages of `MESSAGE` with `Relay`:

- Enables data processing through the relay chain.
- Provides a unified orderId for cross-chain transactions, ensuring clarity in the cross-chain path.
- Allows for more refined handling of cross-chain data.