<script>
import { createEventDispatcher } from 'svelte';
	
const dispatch = createEventDispatcher();

let account = "";
let netv = "";


async function getAccount() {
  const accounts = await ethereum.request({ method: 'eth_accounts' });
  const network_version = await ethereum.request({ method: 'net_version' });
  

   if(network_version == 3) {
        netv = "Ropstein Test Netwoek";
   }

   account = accounts[0];
/*
   Ethereum Main Network (Mainnet)
0x3	3	Ropsten Test Network
0x4	4	Rinkeby Test Network
0x5	5	Goerli Test Network
0x2a	42	Kovan Test Network
*/
  //getValue(account);
  alert(n[netv]);
}


</script>
<button class="bg-blue-500 text-white active:bg-blue-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button" on:click={getAccount}>
    Enable Ethereum
</button>
<h3>Account: <span>{ account }</span></h3>
<h3>Net Version: <span>{ netv }</span></h3>