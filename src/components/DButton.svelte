<script>



async function getAccount() {
  const accounts = await ethereum.request({ method: 'eth_requestAccounts' });
  const account = accounts[0];
  alert(account)
  showAccount.innerHTML = account;
}
</script>

<button type="button" on:click={getAccount}>Enable Ethereum</button>
<h2>Account: <span class="showAccount"></span></h2>