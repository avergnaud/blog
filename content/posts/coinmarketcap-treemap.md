---
title: "Market Cap Treemap"
date: 2020-04-18T20:38:21+02:00
draft: false
imagePreview: "/images/coinmarketcap-treemap-preview.png"
tags: [
    "fintech",
    "D3.js"
]
---

And 24h performance for 10 biggest cryptocurrencies. This project uses the [CoinMarketCap API](https://coinmarketcap.com/api/). 

<!--more-->

## Market Capitalization

The browser first reaches a SpringBoot backend server. This backend calls CoinMarketCap and caches the data (for 30 minutes). The sources for the [backend server](https://github.com/avergnaud/coinmarketcap-px) and for the [d3.JS tree map](https://github.com/avergnaud/blog/blob/master/content/script/coinmarketcap-treemap.js) are available on Github.
The first loading is slow because of:
* Heroku Free plan making the backend "sleep after 30 mins of inactivity"
* The call to coinmarketcap API, once the 30 minutes cache has expired
<div class="first-post-visualisation">
    <div class="lds-container">
        <div class="lds-ring"><div></div><div></div><div></div><div></div></div>
    </div>
</div>
<script src = "/script/coinmarketcap-treemap.js"></script> 

For each rectangle, the area is proportional to the currency's market capitalization. The % figure is the Kraken exchange rate performance for the last 24 hours (EUR market). Colored red when negative, and green when positive.