<!DOCTYPE html>
<html lang="ar" dir="rtl">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>تطبيق الطعام</title>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #f7f7f7;
  color: #222;
}

header {
  background: #ff6b35;
  color: white;
  padding: 25px 20px;
  border-radius: 0 0 25px 25px;
}

.container {
  max-width: 900px;
  margin: auto;
  padding: 18px;
}

h1 {
  margin: 0 0 8px;
}

.search {
  width: 100%;
  padding: 15px;
  border: none;
  border-radius: 14px;
  margin: 18px 0;
  font-size: 16px;
}

.categories {
  display: flex;
  gap: 10px;
  overflow-x: auto;
}

.category {
  border: none;
  background: white;
  padding: 12px 16px;
  border-radius: 20px;
  white-space: nowrap;
  cursor: pointer;
}

.category.active {
  background: #ff6b35;
  color: white;
}

.foods {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 15px;
  margin-top: 20px;
}

.card {
  background: white;
  border-radius: 18px;
  overflow: hidden;
  box-shadow: 0 3px 12px #0001;
}

.image {
  height: 130px;
  background: #eee;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 55px;
}

.info {
  padding: 14px;
}

.info h3 {
  margin: 0 0 8px;
}

.price {
  color: #ff6b35;
  font-weight: bold;
  margin-bottom: 10px;
}

.add {
  width: 100%;
  padding: 10px;
  border: none;
  border-radius: 10px;
  background: #ff6b35;
  color: white;
  cursor: pointer;
}

.cart {
  position: fixed;
  left: 18px;
  bottom: 18px;
  border: none;
  border-radius: 30px;
  background: #222;
  color: white;
  padding: 14px 20px;
  font-size: 16px;
}
</style>
</head>

<body>

<header>
<div class="container">
<h1>🍔 تطبيق الطعام</h1>
<p>اكتشف وجبتك المفضلة واطلبها بسهولة</p>
</div>
</header>

<main class="container">

<input
id="search"
class="search"
placeholder="🔎 ابحث عن وجبة..."
>

<div class="categories">

<button class="category active" data-category="all">
الكل
</button>

<button class="category" data-category="burger">
🍔 برغر
</button>

<button class="category" data-category="pizza">
🍕 بيتزا
</button>

<button class="category" data-category="chicken">
🍗 دجاج
</button>

<button class="category" data-category="drink">
🥤 مشروبات
</button>

</div>

<div id="foods" class="foods"></div>

</main>

<button id="cart" class="cart">
🛒 السلة (0)
</button>

<script>

const foods = [
{
name: "برغر لحم",
category: "burger",
price: 850,
emoji: "🍔"
},
{
name: "بيتزا مارغريتا",
category: "pizza",
price: 1000,
emoji: "🍕"
},
{
name: "دجاج مقرمش",
category: "chicken",
price: 900,
emoji: "🍗"
},
{
name: "بطاطا مقلية",
category: "chicken",
price: 300,
emoji: "🍟"
},
{
name: "بيتزا دجاج",
category: "pizza",
price: 1200,
emoji: "🍕"
},
{
name: "مشروب غازي",
category: "drink",
price: 150,
emoji: "🥤"
},
{
name: "برغر دجاج",
category: "burger",
price: 750,
emoji: "🍔"
},
{
name: "عصير طبيعي",
category: "drink",
price: 350,
emoji: "🧃"
}
];

let selectedCategory = "all";
let cartCount = 0;

function displayFoods() {

const search =
document.getElementById("search").value.toLowerCase();

const container =
document.getElementById("foods");

container.innerHTML = "";

foods
.filter(food =>
(selectedCategory === "all" ||
food.category === selectedCategory) &&
food.name.toLowerCase().includes(search)
)
.forEach(food => {

container.innerHTML += `
<div class="card">

<div class="image">
${food.emoji}
</div>

<div class="info">

<h3>${food.name}</h3>

<div class="price">
${food.price} دج
</div>

<button class="add" onclick="addToCart()">
أضف للسلة
</button>

</div>

</div>
`;

});

}

function addToCart() {

cartCount++;

document.getElementById("cart").textContent =
"🛒 السلة (" + cartCount + ")";

}

document.querySelectorAll(".category")
.forEach(button => {

button.onclick = () => {

document.querySelectorAll(".category")
.forEach(b => b.classList.remove("active"));

button.classList.add("active");

selectedCategory =
button.dataset.category;

displayFoods();

};

});

document.getElementById("search")
.addEventListener("input", displayFoods);

displayFoods();

</script>

</body>
</html>
