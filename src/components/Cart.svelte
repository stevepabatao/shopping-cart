<script>
    export let cartItems;
    $: cartTotal = cartItems.reduce((sum, curValue) => {
      return sum + curValue.price * curValue.quantity;
    }, 0);
    function getSubtotal(item) {
      return item.price * item.quantity;
    }
    function removeItem(id) {
      cartItems = cartItems.filter(function (item) {
        return item.id !== id;
      });
    }
  </script>

  <!--start-->
  <div class="container mx-auto mt-10">
    <div class="flex shadow-md my-10">
      <div class="w-3/4 bg-white px-10 py-10">
        <div class="flex justify-between border-b pb-8">
          <h1 class="font-semibold text-2xl">Shopping Cart</h1>
          <h2 class="font-semibold text-2xl">{cartItems.length} Items</h2>
        </div>
        <div class="flex mt-10 mb-5">
          <h3 class="font-semibold text-gray-600 text-xs uppercase w-2/5">Product Details</h3>
          <h3 class="font-semibold text-center text-gray-600 text-xs uppercase w-1/5 text-center">Quantity</h3>
          <h3 class="font-semibold text-center text-gray-600 text-xs uppercase w-1/5 text-center">Price</h3>
          <h3 class="font-semibold text-center text-gray-600 text-xs uppercase w-1/5 text-center">Total</h3>
        </div>

        {#if cartItems.length === 0}
        <div class="flex items-center hover:bg-gray-100 -mx-8 px-6 py-5"><p>No items in cart yet.</p></div>
        {:else}
    
        {#each cartItems as item}
        <div class="flex items-center hover:bg-gray-100 -mx-8 px-6 py-5">
          <div class="flex w-2/5"> <!-- product -->
            <div class=" object-scale-down h-20">
              <img class="h-24" src="{item.image}" alt="">
            </div>
            <div class="flex flex-col justify-between ml-4 flex-grow">
              <span class="font-bold text-sm">{item.title}</span>
              <a href="/" class="font-semibold hover:text-red-500 text-gray-500 text-xs" on:click={removeItem(item.id)}>Remove</a>
            </div>
          </div>
          <div class="flex justify-center w-1/5">


            <input type="number"  size='3' class="mx-2 border text-center w-8" bind:value={item.quantity}>

          </div>
          <span class="text-center w-1/5 font-semibold text-sm">${item.price}</span>
          <span class="text-center w-1/5 font-semibold text-sm">${getSubtotal(item)}</span>
        </div>
        {/each}
        {/if}
      </div>

      <div id="summary" class="w-1/4 px-8 py-10">



        <h1 class="font-semibold text-2xl border-b pb-8">Order Summary</h1>
        <div class="flex justify-between mt-10 mb-5">
          <span class="font-semibold text-sm uppercase">Items 3</span>
          <span class="font-semibold text-sm">${cartTotal}</span>
        </div>
 
        <div class="border-t mt-8">
          <div class="flex font-semibold justify-between py-6 text-sm uppercase">
            <span>Total cost</span>
            <span>${cartTotal}</span>
          </div>
          <button class="bg-indigo-500 font-semibold hover:bg-indigo-600 py-3 text-sm text-white uppercase w-full">Checkout</button>

        </div>
      </div>

    </div>
  </div>
  <!--end-->
  