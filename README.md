<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SuBri KAG - handmade collections</title>
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;600&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0;font-family:Poppins}
body{background:#fafafa;color:#333}
header{padding:20px;text-align:center;background:#fff;box-shadow:0 2px 6px rgba(0,0,0,0.1)}
.hero{height:90vh;background:url('https://i.ibb.co/5gF2XVSD/woman-posing-jumping-while-holding-shopping-bags.jpg') center/cover no-repeat;display:flex;align-items:center;justify-content:center;flex-direction:column;color:white;text-align:center}
.hero h1{font-size:3rem;background:rgba(0,0,0,0.4);padding:10px 20px;border-radius:10px}
.hero button{margin-top:20px;padding:12px 25px;border:none;background:#ff5a5f;color:#fff;font-size:18px;border-radius:30px;cursor:pointer}
.products{padding:40px}
.carousel{display:flex;gap:20px;overflow-x:auto;padding:20px}
.card{min-width:250px;background:#fff;border-radius:12px;box-shadow:0 3px 10px rgba(0,0,0,0.1);padding:15px;text-align:center}
.card img{width:100%;border-radius:10px}
.card button{margin-top:10px;padding:8px 15px;background:#111;color:#fff;border:none;border-radius:20px;cursor:pointer}
.cart-icon{position:fixed;right:20px;bottom:90px;background:#111;color:#fff;width:60px;height:60px;border-radius:50%;display:flex;align-items:center;justify-content:center;font-size:22px;cursor:pointer}
.cart-count{position:absolute;top:-5px;right:-5px;background:red;color:#fff;border-radius:50%;font-size:12px;padding:4px 7px}
.whatsapp{position:fixed;bottom:20px;right:20px;background:#25D366;width:60px;height:60px;border-radius:50%;display:flex;align-items:center;justify-content:center;color:#fff;font-size:30px;text-decoration:none}
.cart-drawer{position:fixed;right:-400px;top:0;width:350px;height:100%;background:#fff;box-shadow:-3px 0 10px rgba(0,0,0,0.2);padding:20px;transition:0.3s;overflow:auto}
.cart-drawer.open{right:0}
.cart-item{border-bottom:1px solid #eee;padding:10px 0}
.checkout-form input,textarea{width:100%;padding:10px;margin:6px 0;border:1px solid #ddd;border-radius:6px}
.checkout-form button{width:100%;padding:12px;background:#ff5a5f;color:#fff;border:none;border-radius:8px;margin-top:10px}
.qr{width:100%;margin-top:10px}
footer{text-align:center;padding:20px;background:#fff;margin-top:30px}
</style>
</head>
<body>
<header>
<h2>SuBri KAG</h2>
<p>handmade collections</p>
</header>
<section class="hero">
<h1>Discover Handmade Fashion</h1>
<button onclick="document.getElementById('products').scrollIntoView({behavior:'smooth'})">Shop Now</button>
</section>
<section id="products" class="products">
<h2>Products</h2>
<div class="carousel">
<div class="card">
<img src="https://i.ibb.co/TJ09Kzk/Whats-App-Image-2026-03-13-at-3-23-27-PM-1.jpg">
<h3>Handmade Piece 1</h3>
<p>₹799</p>
<button onclick="addToCart('Handmade Piece 1',799)">Add to Cart</button>
</div>
<div class="card">
<img src="https://i.ibb.co/bjq7hPBq/Whats-App-Image-2026-03-14-at-3-27-47-PM.jpg">
<h3>Handmade Piece 2</h3>
<p>₹899</p>
<button onclick="addToCart('Handmade Piece 2',899)">Add to Cart</button>
</div>
<div class="card">
<img src="https://i.ibb.co/9kTgPpQ4/Whats-App-Image-2026-03-14-at-3-03-12-PM.jpg">
<h3>Handmade Piece 3</h3>
<p>₹999</p>
<button onclick="addToCart('Handmade Piece 3',999)">Add to Cart</button>
</div>
<div class="card">
<img src="https://i.ibb.co/G3TQsbKn/Whats-App-Image-2026-03-14-at-3-01-05-PM.jpg">
<h3>Handmade Piece 4</h3>
<p>₹1099</p>
<button onclick="addToCart('Handmade Piece 4',1099)">Add to Cart</button>
</div>
</div>
</section>
<div class="cart-icon" onclick="toggleCart()">🛒<span class="cart-count" id="cartCount">0</span></div>
<a class="whatsapp" href="https://wa.me/8799749343">💬</a>
<div class="cart-drawer" id="cartDrawer">
<h2>Your Cart</h2>
<div id="cartItems"></div>
<h3>Customer Details</h3>
<form class="checkout-form" id="orderForm">
<input type="text" id="name" placeholder="Full Name" required>
<input type="tel" id="phone" placeholder="Phone Number" required>
<textarea id="address" placeholder="Full Address" required></textarea>
<input type="text" id="pincode" placeholder="Pincode" required>
<p><b>Payment:</b> COD not available. Pay using Paytm QR below.</p>
<img class="qr" src="https://i.ibb.co/g2VMMkZ/Whats-App-Image-2026-03-14-at-9-46-43-PM.jpg">
<p>After Paytm payment, your order details will be sent to brand email.</p>
<button type="submit">Send Order</button>
</form>
</div>
<footer>
<p>Founder: Anjali Brij Kushwaha</p>
<p>Email: subrikag2712@gmail.com</p>
</footer>
<script src="https://cdn.jsdelivr.net/npm/emailjs-com@3/dist/email.min.js"></script>
<script>
emailjs.init("YOUR_PUBLIC_KEY");
let cart=[];
function addToCart(name,price){
cart.push({name,price});
updateCart();
}
function updateCart(){
document.getElementById('cartCount').innerText=cart.length;
let itemsHTML="";
cart.forEach(item=>{
itemsHTML+=`<div class='cart-item'>${item.name} - ₹${item.price}</div>`;
});
document.getElementById('cartItems').innerHTML=itemsHTML;
}
function toggleCart(){
document.getElementById('cartDrawer').classList.toggle('open');
}
document.getElementById('orderForm').addEventListener('submit',function(e){
e.preventDefault();
let name=document.getElementById('name').value;
let phone=document.getElementById('phone').value;
let address=document.getElementById('address').value;
let pincode=document.getElementById('pincode').value;
let items=cart.map(i=>`${i.name} - ₹${i.price}`).join(', ');
emailjs.send("YOUR_SERVICE_ID","YOUR_TEMPLATE_ID",{
customer_name:name,
phone:phone,
address:address,
pincode:pincode,
order_items:items
}).then(()=>{
alert("Order sent successfully!");
cart=[];
updateCart();
});
});
</script>
</body>
</html>
