<script>    
import { ethers } from 'ethers';

import TokenArtifact from "./contracts/Token.json";
import contractAddress from "./contracts/contract-address.json";

//const HARDHAT_NETWORK_ID = '31337';
const HARDHAT_NETWORK_ID = '3';
const ERROR_CODE_TX_REJECTED_BY_USER = 4001;

let selectedAddress = ''; 
let networkError = null;

let token = null;
let balance = null;
let pollDataInterval = null;
let provider = null; 
let tokenData = null;

function initialize(userAddress) {
    // This method initializes the dapp

    // We first store the user's address in the component's state
    selectedAddress = userAddress,

    // Then, we initialize ethers, fetch the token's data, and start polling
    // for the user's balance.

    // Fetching the token data and the user's balance are specific to this
    // sample project, but you can reuse the same initialization pattern.
    intializeEthers();
    getTokenData();
    startPollingData();
  }

  async function intializeEthers() {
    // We first initialize ethers by creating a provider using window.ethereum
    provider = new ethers.providers.Web3Provider(window.ethereum);

    // When, we initialize the contract using that provider and the token's
    // artifact. You can do this same thing with your contracts.
    token = new ethers.Contract(
      contractAddress.Token,
      TokenArtifact.abi,
      provider.getSigner(0)
    );

    console.log(token);
  }  

  async function getTokenData() {
    const name = await token.name();
    const symbol = await token.symbol();

    tokenData: { name, symbol };

    console.log(tokenData);
  }


  function checkNetwork() {
    if (window.ethereum.networkVersion === HARDHAT_NETWORK_ID) {
      return true;
    }
    networkError = 'Please connect Metamask to Localhost:8545'
    return false;
  }

  async  function updateBalance() {
     balance = await token.balanceOf(selectedAddress);
     console.log("Balance:" + balance);
  }

    // The next to methods are needed to start and stop polling data. While
  // the data being polled here is specific to this example, you can use this
  // pattern to read any data from your contracts.
  //
  // Note that if you don't need it to update in near real time, you probably
  // don't need to poll it. If that's the case, you can just fetch it when you
  // initialize the app, as we do with the token data.
  function startPollingData() {
     pollDataInterval = setInterval(() => updateBalance(), 10000);

    // We run it once immediately so we don't have to wait for it
    console.log("Poll address;" + selectedAddress);
    updateBalance();
  }

  function stopPollingData() {
    clearInterval(pollDataInterval);
    pollDataInterval = undefined;
  }


  async function connectWallet() {
    // This method is run when the user clicks the Connect. It connects the
    // dapp to the user's wallet, and initializes it.

    // To connect to the user's wallet, we have to run this method.
    // It returns a promise that will resolve to the user's address.
    const [selectedAddress] = await window.ethereum.enable();
    console.log("Address:" + selectedAddress);

    // Once we have the address, we can initialize the application.

    // First we check the network
    if (!checkNetwork()) {
      return;
    }

    initialize(selectedAddress);

    // We reinitialize it whenever the user changes their account.
    window.ethereum.on("accountsChanged", ([newAddress]) => {
      stopPollingData();
      // `accountsChanged` event can be triggered with an undefined newAddress.
      // This happens when the user removes the Dapp from the "Connected
      // list of sites allowed access to your addresses" (Metamask > Settings > Connections)
      // To avoid errors, we reset the dapp state 
      if (newAddress === undefined) {
        return newAddres = null;
      }
      
      initialize(newAddress);
    });
    
    // We reset the dapp state if the network is changed
    window.ethereum.on("networkChanged", ([networkId]) => {
      stopPollingData();
      //this._resetState();
    });
  }


  async function transferTokens() {
    // Sending a transaction is a complex operation:
    //   - The user can reject it
    //   - It can fail before reaching the ethereum network (i.e. if the user
    //     doesn't have ETH for paying for the tx's gas)
    //   - It has to be mined, so it isn't immediately confirmed.
    //     Note that some testing networks, like Hardhat Network, do mine
    //     transactions immediately, but your dapp should be prepared for
    //     other networks.
    //   - It can fail once mined.
    //
    // This method handles all of those things, so keep reading to learn how to
    // do it.
    let transactierroronError = null;
    //let txBeingSent = null; 



    try {
      const to = '0xFfc3a2baBDC923f687EcE7192a6C6f08D05CE826';
      const amount = 100;
      // If a transaction fails, we save that error in the component's state.
      // We only save one such error, so before sending a second transaction, we
      // clear it.
      dismissTransactionError();

      // We send the transaction, and save its hash in the Dapp's state. This
      // way we can indicate that we are waiting for it to be mined.
      const tx = await token.transfer(to, amount);
      //const txBeingSent = tx.hash;

     // console.log(txBeingSe);

      // We use .wait() to wait for the transaction to be mined. This method
      // returns the transaction's receipt.
      const receipt = await tx.wait();

      // The receipt, contains a status flag, which is 0 to indicate an error.
      if (receipt.status === 0) {
        // We can't know the exact error that make the transaction fail once it
        // was mined, so we throw this generic one.
        throw new Error("Transaction failed");
      }

      // If we got here, the transaction was successful, so you may want to
      // update your state. Here, we update the user's balance.
      await updateBalance();
    } catch (error) {
      // We check the error code to see if this error was produced because the
      // user rejected a tx. If that's the case, we do nothing.
      if (error.code === ERROR_CODE_TX_REJECTED_BY_USER) {
        return;
      }

      // Other errors are logged and stored in the Dapp's state. This is used to
      // show them to the user, and for debugging.
      console.log(error);
      transactierroronError = error;
    } finally {
      // If we leave the try/catch, we aren't sending a tx anymore, so we clear
      // this part of the state.
      //txBeingSent = undefined;
    }
  }

   // This method just clears part of the state.
  function dismissTransactionError() {
    const transactionError = undefined;
  }

  // This method just clears part of the state.
  function dismissNetworkError() {
    const networkError = undefined;
  }

  // This is an utility method that turns an RPC error into a human readable
  // message.
  function getRpcErrorMessage(error) {
    if (error.data) {
      return error.data.message;
    }

    return error.message;
  }


</script>

    <div class="max-w-lg rounded-lg shadow-lg p-4 float-right">
        <div class="font-semibold text-md text-gray-700 tracking-wide">Connection</div>
            <ul>
                <li><span class="text-xs">Account: <span class="font-weight-700">{ selectedAddress }</span></span></li>
                <li><span class="text-xs">Balance: <span class="font-weight-700">{ balance }</span></span></li>
            </ul>
        <div>
            <button class="bg-blue-500 text-white active:bg-blue-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button" on:click={connectWallet}>
                Enable Ethereum
            </button>
            <button class="bg-blue-500 text-white active:bg-blue-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button" on:click={transferTokens}>
                Send Ethereum
            </button>
            
        </div>
    </div>
