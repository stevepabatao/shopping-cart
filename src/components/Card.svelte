<script>
    import { createEventDispatcher } from "svelte";
    import Button from "./Button.svelte";
    export let productId;
    export let productTitle;
    export let productPrice;
    export let productImage;
    const dispatch = createEventDispatcher();
    function addToCart() {
      dispatch("addcart", productId);
    }
  </script>




<div class="wrapper bg-gray-100 antialiased text-gray-900 p-6 w-64 mx-8">
<div>
    
    <img src="{productImage}" alt=" random imgee" class="w-full object-cover h-48 w-full object-center rounded-lg shadow-md">    
    
 <div class="relative px-1 -mt-16  ">
   <div class="bg-white p-6 rounded-lg shadow-lg">

    
    <h4 class="mt-1 text-xl font-semibold uppercase leading-tight truncate">{productTitle}</h4>
 
  <div class="mt-1">
    $
    <span></span>
    <span class="text-gray-600 text-sm">{productPrice}</span>
  </div>
  <div class="mt-4">
 
    <span class="text-sm text-gray-600">    
      <slot name="description">
        <p>No description</p>
      </slot>
    </span>
    
  </div>  
  <Button on:click={addToCart}>Add to Cart</Button>

  </div>
 </div>
 <div class="justify-center">
 
 </div>
</div>
  </div>



  
  <!--
  <div class="bg-gray rounded shadow border p-6 w-64 mx-8">
    <img class="object-scale-down h-48 w-full" src={productImage} alt="Product" />
    <h1>{productTitle}</h1>
    <slot name="description">
      <p>No description</p>
    </slot>
    <p class="price">
      $
      <span>{productPrice}</span>
    </p>
    <p>
      <Button on:click={addToCart}>Add to Cart</Button>
    </p>
  </div>
-->