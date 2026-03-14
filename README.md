<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>News Explorer</title>
</head>

<body>

<h2>Tech News</h2>

<p>
<button class="topic" data-topic="DS">DS</button>
<button class="topic" data-topic="AIML">AIML</button>
<button class="topic" data-topic="AI">AI</button>
<button class="topic" data-topic="javascript">Javascript</button>
</p>

<hr>

<div id="news"></div>

<script>

const newsContainer = document.getElementById("news");
const buttons = document.querySelectorAll(".topic");

async function fetchnews(topic){

const url = `https://hn.algolia.com/api/v1/search?query=${topic}`;

newsContainer.innerHTML = "Loading...";

try{

const response = await fetch(url);
const data = await response.json();

showNews(data.hits);

}catch(error){
newsContainer.innerHTML = "Error loading news";
}

}

function showNews(articles){

newsContainer.innerHTML = "";

articles.forEach(article => {

const title = article.title || article.story_title;
const url = article.url || article.story_url;

if(!title || !url) return;

const div = document.createElement("div");

div.innerHTML = `
<p>
<a href="${url}" target="_blank">${title}</a>
</p>
`;

newsContainer.appendChild(div);

});

}

buttons.forEach(button => {

button.addEventListener("click", () => {

const topic = button.dataset.topic;
fetchnews(topic);

});

});

</script>

</body>
</html># article_project-08
