<template>
    <div>
        <div v-for="product in products" :key="product.id">
            <h2>{{product.title}}</h2>
            <figure>
                <img v-bind:src="product.image"/>
            </figure>
            <p v-html="product.description"></p>
            <p>Price: {{product.price}}</p>
            <p>Availible stock: {{product.availibleInventory}}</p>
            <button @click="add(product)">Add to cart</button>
        </div>
    </div>
    </template>
    <script>
    export default {
        name: "ProductList",
        data() {
            return{
                products: [
                {
  
  id: 1001,
  title: "Xiaomi 12T",
  description: "The Xiaomi 12T is a 5G smartphone with a 6.67-inch AMOLED display, Mediatek Dimensity 8100 Ultra processor, 108MP main camera, and 5000mAh battery.",
  price: 1500,
  image: "images/Phone.jpg",
  availableInventory: 5,
  rating: 5
},
{
  id: 1002,
  title: "Soundcore life p3",
  description: "Soundcore Life P3 are noise-cancelling earbuds with 11mm drivers, BassUp technology, 6 mics, and wireless charging.",
  price: 250,
  image: "images/Earbuds.jpg",
  availableInventory: 5,
  rating: 4
},
{
  id: 1003,
  title: "Samsung Galaxy watch 4",
  description: "The Galaxy Watch 4 is a Wear OS smartwatch with a 1.4 inch display, Exynos W920 chipset, and health monitoring.",
  price: 700,
  image: "images/Watch.jpg",
  availableInventory: 5,
  rating: 3
},
{
  id: 1004,
  title: "Acer Nitro 5",
  description: "The Acer Nitro 5 is an Intel i7-powered gaming laptop with NVIDIA GeForce RTX 3070Ti graphics and a 15.6 inch display.",
  price: 3000,
  image: "images/Laptop.jpg",
  availableInventory: 5,
  rating: 3
},
{
  id: 1005,
  title: "Nikon D7500",
  description: "The Nikon D7500 is a 20.9 MP DSLR camera with high ISO capabilities for low light photography, fast EXPEED 5 image processing, energy efficiency, and a tilt-angle touchscreen.",
  price: 5000,
  image: "images/Camera.jpg",
  availableInventory: 5,
  rating: 3
},
{
  id: 1006,
  title: "Sony Wireless Headset",
  description: "The Sony WH-CH520 is a lightweight, wireless headphone with volume control and Bluetooth connectivity.",
  price: 150,
  image: "images/headphones.jpg",
  availableInventory: 5,
  rating: 3
},
{
  id: 1007,
  title: "Razer Mouse",
  description: "The Razer DeathAdder Essential is a right-handed gaming mouse with 6400 DPI, 5 programmable buttons, and 1000Hz Ultrapolling.",
  price: 125,
  image: "images/mouse.jpg",
  availableInventory: 5,
  rating: 3
},
{
  id: 1008,
  title: "Sony C700n earbuds",
  description: "The Sony WF-C700N is a truly wireless, noise-cancelling earbud with superior audio quality and a built-in microphone.",
  price: 255,
  image: "images/sonyearbuds.jpg",
  availableInventory: 5,
  rating: 3
},
{
  id: 1009,
  title: "Soundcore Speaker",
  description: "The Soundcore Mini 3 is a compact, 360° Bluetooth speaker with customizable sound via the Soundcore app.",
  price: 70,
  image: "images/speaker.jpg",
  availableInventory: 5,
  rating: 3
},
{
  id: 1010,
  title: "Mi buds 3 pro",
  description: "The Mi Buds 3 Pro are truly wireless earbuds with 35dB noise cancellation, dual-device connectivity, and wireless charging.",
  price: 300,
  image: "images/Buds.jpg",
  availableInventory: 5,
  rating: 3
},
                ],
            };
        },
        methods:{
            add(product) {
                console.log("added product", product.id);
                this.$emit('addProduct',product);
            },
        },
    };
    </script>