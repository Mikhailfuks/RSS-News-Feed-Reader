const feedUrlInput = document.getElementById('feed-url');
const fetchButton = document.getElementById('fetch-button');
const newsContainer = document.getElementById('news-container');

fetchButton.addEventListener('click', fetchRSSFeed);

function fetchRSSFeed() {
  const feedUrl = feedUrlInput.value.trim();

  if (feedUrl === '') {
    alert('Please enter a valid RSS feed URL.');
    return;
  }

  fetch(https://api.rss2json.com/v1/api.json?rss_url=${encodeURIComponent(feedUrl)})
    .then(response => response.json())
    .then(data => displayNews(data))
    .catch(error => {
      console.error('Error fetching feed:', error);
      displayError('An error occurred while fetching the feed. Please try again later.');
    });
}

function displayNews(data) {
  newsContainer.innerHTML = ''; // Clear previous news

  if (data.items.length === 0) {
    displayError('No news found.');
    return;
  }

  data.items.forEach(item => {
    const newsItem = document.createElement('div');
    newsItem.innerHTML = 
      <h3><a href="${item.link}">${item.title}</a></h3>
      <p>${item.pubDate}</p>
      <p>${item.description}</p>
    ;
    newsContainer.appendChild(newsItem);
  });
}

function displayError(message) {
  const errorElement = document.createElement('p');
  errorElement.textContent = message;
  errorElement.classList.add('error');
  newsContainer.appendChild(errorElement);
}

// HTML Structure (index.html)
// Add this within your <body> tag:
