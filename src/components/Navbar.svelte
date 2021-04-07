<script>
    import { createEventDispatcher } from "svelte";
    import DButton from './DButton.svelte';
    export let cartItems;
    $: cartLength = cartItems.length;
    let activeLink = "home";
    const dispatch = createEventDispatcher();
    function cartClicked() {
      dispatch("cartclicked", true);
      activeLink = "cart";
    }
    function homeClicked() {
      dispatch("homeclicked", false);
      activeLink = "home";
    }
  </script>

<div class="flex 
            flex-wrap 
            py-2">
    <div class="w-full 
                px-4">
      <nav class="relative 
                  flex 
                  flex-wrap 
                  items-center 
                  justify-between 
                  px-2 py-3 
                  bg-gray-200 
                  rounded">
        <div class="container 
                    px-4 
                    mx-auto 
                    flex 
                    flex-wrap 
                    items-center 
                    justify-between">
          <div class="w-full relative flex justify-between lg:w-auto px-4 lg:static lg:block lg:justify-start">
            <a class="text-sm font-bold leading-relaxed inline-block mr-4 py-2 whitespace-nowrap uppercase text-gray-500" href="/">
              D Cart
            </a>
            <button class="cursor-pointer text-xl leading-none px-3 py-1 border border-solid border-transparent rounded bg-transparent block lg:hidden outline-none focus:outline-none" type="button">
              <span class="block relative w-6 h-px rounded-sm bg-white"></span>
              <span class="block relative w-6 h-px rounded-sm bg-white mt-1"></span>
              <span class="block relative w-6 h-px rounded-sm bg-white mt-1"></span>
            </button>
          </div>
          <div class="flex lg:flex-grow items-center" id="example-navbar-info">
            <ul class="flex flex-col lg:flex-row list-none ml-auto">
              <li class="nav-item">
                <a href="#cart" role="button" class="relative flex">
                    <svg class="flex-1 w-8 h-8 fill-current" viewbox="0 0 24 24">
                      <path d="M17,18C15.89,18 15,18.89 15,20A2,2 0 0,0 17,22A2,2 0 0,0 19,20C19,18.89 18.1,18 17,18M1,2V4H3L6.6,11.59L5.24,14.04C5.09,14.32 5,14.65 5,15A2,2 0 0,0 7,17H19V15H7.42A0.25,0.25 0 0,1 7.17,14.75C7.17,14.7 7.18,14.66 7.2,14.63L8.1,13H15.55C16.3,13 16.96,12.58 17.3,11.97L20.88,5.5C20.95,5.34 21,5.17 21,5A1,1 0 0,0 20,4H5.21L4.27,2M7,18C5.89,18 5,18.89 5,20A2,2 0 0,0 7,22A2,2 0 0,0 9,20C9,18.89 8.1,18 7,18Z"/>
                      </svg>
                      <span class="absolute right-0 top-0 rounded-full bg-red-600 w-4 h-4 top right p-0 m-0 text-white font-mono text-sm  leading-tight text-center">
                         {cartLength}
                    </span>
                  </a>
              </li>
              <li class="nav-item">
                
              </li>  
            </ul>
          </div>
        </div>
      </nav>
    </div>
  </div>
  <div class="flex flex-wrap right py-2  right-0">
    <DButton/> 
  </div>

