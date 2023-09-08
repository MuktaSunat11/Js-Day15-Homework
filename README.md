# Image Search

This is a simple image search engine that allows users to search for images on the web.

# Html file
```
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Image Search</title>
    <link rel="stylesheet" href="style.css" />
  </head>
  <body>
    <h1>Image Search</h1>
    <form>
      <input type="text" id="search-input" placeholder="Search for images..." />
      <button id="search-button">Search</button>
    </form>
    <div class="search-results">
     
 
    
    </div>
    <button id="show-more-button">Show more</button>
    <script src="script.js"></script>
  </body>
</html>
```

# Css file
```
*{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
body {
    background-color: #f9f9f9;
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.6;
    margin: 0;
  }
  
  h1 {
    font-size: 36px;
    font-weight: bold;
    text-align: center;
    margin-top: 40px;
    margin-bottom: 60px;
  }
  
  form {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-bottom: 60px;
  }
  
  #search-input {
    width: 60%;
    max-width: 400px;
    padding: 10px 20px;
    border: none;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
    border-radius: 5px;
    font-size: 18px;
    color: #333;
  }
  
  #search-button {
    padding: 10px 20px;
    background-color: #4caf50;
    color: white;
    border: none;
    font-size: 18px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
    cursor: pointer;
    border-radius: 5px;
    transition: background-color 0.3s ease-in-out;
  }
  
  #search-button:hover {
    background-color: #3e8e41;
  }
  
  .search-results {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    max-width: 1200px;
    margin: 0 auto;
    padding: 20px;
  }
  
  .search-result {
    margin-bottom: 60px;
    width: 30%;
    border-radius: 5px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
    overflow: hidden;
  }
  
  .search-result:hover img {
    transform: scale(1.05);
  }
  
  .search-result img {
    width: 100%;
    height: 200px;
    object-fit: cover;
    transition: transform 0.3s ease-in-out;
  }
  .search-result a {
    padding: 10px;
    display: block;
    color: #333;
    text-decoration: none;
    transition: background-color 0.3s ease-in-out;
  }
  
  .search-result:hover a {
    background-color: rgba(0, 0, 0, 0.1);
  }
  
  #show-more-button {
    background-color: #008cba;
    border: none;
    color: white;
    padding: 10px 20px;
    display: block;
    margin: 20px auto;
    text-align: center;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease-in-out;
    display: none;
  }
  
  #show-more-button:hover {
    background-color: #0077b5;
  }
  ```

# Javascript file
```
const accessKey = "RZEIOVfPhS7vMLkFdd2TSKGFBS4o9_FmcV1Nje3FSjw";

const form = document.querySelector("form");
const searchInput = document.getElementById("search-input");
const searchResults = document.querySelector(".search-results");
const showMoreButton = document.getElementById("show-more-button");

let inputData = "";
let page = 1;

async function searchImages() {
  inputData = searchInput.value;
  const url = `https://api.unsplash.com/search/photos?page=${page}&query=${inputData}&client_id=${accessKey}`;

  const response = await fetch(url);
  const data = await response.json();
  if (page === 1) {
    searchResults.innerHTML = "";
  }

  const results = data.results;

  results.map((result) => {
    const imageWrapper = document.createElement("div");
    imageWrapper.classList.add("search-result");
    const image = document.createElement("img");
    image.src = result.urls.small;
    image.alt = result.alt_description;
    const imageLink = document.createElement("a");
    imageLink.href = result.links.html;
    imageLink.target = "_blank";
    imageLink.textContent = result.alt_description;

    imageWrapper.appendChild(image);
    imageWrapper.appendChild(imageLink);
    searchResults.appendChild(imageWrapper);
  });

  page++;

  if (page > 1) {
    showMoreButton.style.display = "block";
  }
}

form.addEventListener("submit", (event) => {
  event.preventDefault();
  page = 1;
  searchImages();
});

showMoreButton.addEventListener("click", () => {
  searchImages();
});
```
