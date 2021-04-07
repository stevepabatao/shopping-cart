<script>

let account = "";
let netv = "";


async function sendEther() {
    ethereum
        .request({
        method: 'eth_sendTransaction',
        params: [
            {
            from: account,
            to: '0x0F49e71bC4FcA91E020F60f094c02B2Cf7b42561',
            value: '0x29a2241af62c0000',
            gasPrice: '0x09184e72a000',
            gas: '0x2710',
            },
        ],
        })
        .then((txHash) => console.log(txHash))
        .catch((error) => console.error);
}

async function getAccount() {
   const accounts = await ethereum.request({ method: 'eth_requestAccounts' });
   const network_version = await ethereum.request({ method: 'net_version' });

   if(network_version == 3) {
        netv = "Ropstein Test Network";
   }

   account = accounts[0];
}

</script>

    <div class="max-w-lg rounded-lg shadow-lg p-4 float-right">
        <div class="font-semibold text-md text-gray-700 tracking-wide">Connection</div>
            <ul>
                <li><span class="text-xs">Account: <span class="font-weight-700">{ account }</span></span></li>
                <li><span class="text-xs">Net Version: <span class="font-weight-700">{ netv }</span></span></li>
            </ul>
        <div>
            <button class="bg-blue-500 text-white active:bg-blue-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button" on:click={getAccount}>
                Enable Ethereum
            </button>
            <button class="bg-blue-500 text-white active:bg-blue-600 font-bold uppercase text-xs px-4 py-2 rounded shadow hover:shadow-md outline-none focus:outline-none mr-1 mb-1 ease-linear transition-all duration-150" type="button" on:click={sendEther}>
                Send Ethereum
            </button>
            
        </div>
    </div>
