
<script>
	import { v4 as uuidv4 } from "uuid";
	import Tailwind from "./components/Tailwind.svelte";
	import Navbar from "./components/Navbar.svelte";
	import Card from "./components/Card.svelte";
	import Cart from "./components/Cart.svelte";

	let displayCart = false;
	let cartItems = [];
	let products = [
	  {
		id: uuidv4(),
		title: "Camera",
		description: "Capture memories. Buy it now.",
		price: 24000.0,
		image: "./images/camera.jpg",
	  },
	  {
		id: uuidv4(),
		title: "Headphone",
		description: "This is a car. Drive the car.",
		price: 1500.0,
		image: "./images/headphone.jpg",
	  },
	  {
		id: uuidv4(),
		title: "Watch",
		description: "This is a house. Buy the house.",
		price: 11000.0,
		image: "./images/watch.jpg",
	  },
	  {
		id: uuidv4(),
		title: "Polaroid",
		description: "This is a house. Buy the house.",
		price: 8000.0,
		image: "./images/polaroid.jpg",
	  },
	];

	function cartClicked(event) {
	  displayCart = event.detail;
	}

	function homeClicked(event) {
	  displayCart = event.detail;
	}

	
	function addToCart(event) {
	  const selectedProdId = event.detail;
	  const isAlreadyInCart = cartItems.findIndex(
		(prod) => prod.id === selectedProdId
	  );
	  if (isAlreadyInCart > -1) {
		cartItems[isAlreadyInCart].quantity += 1;
	  } else {
		cartItems = [
		  ...cartItems,
		  { ...products.find((prod) => prod.id === selectedProdId), quantity: 1 },
		];
	  }
	}

	window.addEventListener('load', function() {

		if (typeof window.ethereum !== 'undefined') {
			console.log("Metaamask is installed.");
		}
  
	});




  </script>

  <Tailwind/>
  
  
  <Navbar
	on:cartclicked={cartClicked}
	on:homeclicked={homeClicked}
	bind:cartItems />
  

	<div class="flex my-10 justify-center" >
	  {#each products as product}
		<Card
		  on:addcart={addToCart}
		  productId={product.id}
		  productTitle={product.title}
		  productPrice={product.price}
		  productImage={product.image}>
		  <p slot="description">{product.description}</p>
		</Card>
	  {/each}
	</div>

	<div >
		<Cart bind:cartItems />
	</div>
  