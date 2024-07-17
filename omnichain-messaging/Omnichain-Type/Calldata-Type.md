## MessageType:CALLDATA

Example Requirement: You need to obtain the value corresponding to a key from the `dictionaryList` on chain A, and then pass the key and its corresponding value to chain B for storage, so that chain B can also retrieve the value corresponding to the key.

Necessary Conditions:

1. Encode the call data before initiating the cross-chain request.
2. On the source chain, the Omni service interface and contract address are needed to initiate a cross-chain event.
3. On the target chain, the Omni service contract must be granted permission to execute the call method.

We initiate a cross-chain event on source chain A.

```
"@butternetwork/omniservice/contracts/interface/IMOSV3.sol";

contract A {
    //The contract address of OmniService on chain A
    IMOSV3 public imosv3;
    
    mapping(string => string) public dictionaryList;
    
    mapping(address => bool) public whitelist;
    
    function setDictionaryEntry(
    	string memory _key, 
    	string memory _val
    ) external {
    
    }
    
   	function sendDictionaryCalldata(
        uint256 _tochainId, //The chain ID of the target chain.
        bytes memory _target, //The contract address on the target chain.
        string memory _key //The message key on chain A.
    ) external payable {
    	//Encode the message that needs to be cross-chain.
        bytes memory data = abi.encodeWithSelector(A.setDictionaryEntry.selector,_key,dictionaryList[_key]);
                		
        IMOSV3.MessageData memory mData = IMOSV3.MessageData(
            false,
            IMOSV3.MessageType.CALLDATA, ///Select CALLDATA for cross-chain transmission.
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

After `messager` detects the cross-chain log, it will execute the cross-chain message on chain B.

We implement `mapoExecute` on chain B to finalize the cross-chain message execution.

```
"@butternetwork/omniservice/contracts/interface/IMOSV3.sol";

contract B is IMapoExecutor {
    //The contract address of OmniService on chain B
    IMOSV3 public imosv3;
    
	mapping(bytes32 => bool) orderList;
	
	//In a simple example, here's a mapping used to store cross-chain data 
	//(this can be any other type, this is just a simple example)
	mapping(string => string) public dictionary;
	
	function setDictionaryEntry(
    	string memory _key, 
    	string memory _val
    ) external {
        require(whitelist[msg.sender], "access denied");
        dictionary[_key] = _val;
        emit setEntry(_key, _val);
        return true;
    }
	//Grant or revoke permission for the contract address on the source chain. 
	//True indicates permission granted, and false indicates no permission.
	function addRemoteCaller(
		uint256 _fromChain, 
		bytes memory _fromAddress, 
		bool _tag
	) external {
        imosv3.addRemoteCaller(_fromChain, _fromAddress, _tag);
    }
}
```

Advantages of `CALLDATA`:
- Cross-chain data is predetermined.
- The target chain does not require extensive contract checks; granting Omni service execution permission is sufficient.

