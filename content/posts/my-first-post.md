---
title: "Market Cap Treemap"
date: 2020-04-18T20:38:21+02:00
draft: true
imagePreview: "/images/my-first-post-preview.png"
tags: [
    "fintech",
    "D3.js",
]
---

And 24h performance for 10 biggest crypto coins. This project uses the [CoinMarketCap API](https://coinmarketcap.com/api/). 

<!--more-->

## Market Capitalization

The browser first reaches a SpringBoot backend server. This backend calls CoinMarketCap and caches the data (for 30 minutes). The sources for the backend server [are available on Github](https://github.com/avergnaud/coinmarketcap-px)
<div class="first-post-visualisation">
    <div class="lds-container">
        <div class="lds-ring"><div></div><div></div><div></div><div></div></div>
    </div>
</div>
<script src = "https://cdnjs.cloudflare.com/ajax/libs/d3/5.15.0/d3.js"></script>
<script src = "/script/my-first-post.js"></script> 