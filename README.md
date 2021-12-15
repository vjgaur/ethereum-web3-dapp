# Dapp Summary
Metamask injects a web3 Object if it is enabled for the browser

If application finds there is no injected web3 object it would create a new web3 object by providing the JSONRPC url end point using below code

```
    var provider = document.getElementById('provider_url').value;
    window.web3 = new Web3(new Web3.providers.HttpProvider(provider));
```

App Can check whether app is connected to Ethereum Node or not by using

```
    web3.isConnected() //returns true if connected
```

# Getting Node Information
(Runtime Status of Node)
Listening
Peer Count
Synching
Mining
Version Information
# > web.version
```
function  setWeb3Version() {

    var versionJson = {};

    // Asynchronous version receiving the node information
    web3.version.getNode(function(error, result){
        if(error) setData('version_information',error,true);
        else {
            setData('version_information',result,false);

            if(result.toLowerCase().includes('metamask')){
                nodeType = 'metamask';
            } else if(result.toLowerCase().includes('testrpc')){
                nodeType = 'testrpc';
            } else {
                nodeType = 'geth';
            }

            
            // set up UI elements based on the node type
            setUIBasedOnNodeType();
        }
    });

   
   {
       api: "0.15.3",
       ethereum: "0x3f"
       network: "3"
       node: "Geth/v1.5.6-stable-2a609af5/windows/gol.7.4"
       whisper:undefined,
       getEthereum: function(callback),
       getNetwork: function(callback),
       getNode: function(callback),
       getWhisper: function(callback)
   }
```
# > web3.net to find out if node is listening to peer connection or not
```
listening / getListening function
peerCount/getPeerCount

function    doGetNodeStatus()  {

    // Asynch version
    web3.net.getListening(function(error, result){
        if(error) setData('get_peer_count',error,true);
        else {
            // Since connected lets get the count
            web3.net.getPeerCount(  function(  error,  result ) {
            if(error){
                setData('get_peer_count',error,true);
            } else {
                setData('get_peer_count','Peer Count: '+result,(result == 0));
            }
        });
        }
    });
}
```

# Node Syncing Status
The Ethereum node connects to other nodes to get the information about blocks that is the syncing part of node.
## web3.isSyncing(callback)
## web3.synching/getSyncing
```
{
    startingBlock:300,
    currentBlock:312,
    highestBlock:512
}
```
## web3.mining/getMining 
The API returns true if the node is mining or false otherwise. You can start and stop mining by using these methods.

