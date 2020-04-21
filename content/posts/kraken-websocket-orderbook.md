---
title: "Live Order Book"
date: 2020-04-19T11:01:22+02:00
draft: true
imagePreview: "/images/kraken-websocket-orderbook-preview.png"
tags: [
    "fintech",
    "D3.js",
]
---

Live data from Kraken Websocket API showing the Order Book. 

See the [demo](https://kraken-orders.herokuapp.com/) on Heroku...

<!--more-->

<img src="/images/kraken-websocket-orderbook-preview.png" style="max-width: 100%;">

## ETHEUR Order Book

See the [sources on Github](https://github.com/avergnaud/wss-kraken-orders)

The browser does not request directly the Kraken API. Instead it opens a websocket connexion with an intermediate Node.js server. This server also requests Kraken through its Websocket API (see [kraken-client.js](https://github.com/avergnaud/wss-kraken-orders/blob/master/server/kraken-client.js)). The server does not send a message to the browser on each incoming message from Kraken. It uses RxJS debouce operator to wait at least for 100ms (see [this](https://github.com/avergnaud/wss-kraken-orders/blob/master/server/server.js)), thus letting enough time for D3js to display smooth animations.

Here is a quick reminder [from Kraken](https://support.kraken.com/hc/en-us/articles/115000364388-Trading-glossary) about the Bid/Ask depth :
* _Bid_: "An order listed on the buy side of the order book". The volume of those orders are sumed in the green rectangles of the order book. 
* _Ask_: "n order listed on the sell side of the order book". The volume of those orders are sumed in the red rectangles of the order book. 
* _Bid/Ask Depth_: "The Bid/Ask Depth represents the cumulative volume of buy and sell orders at a particular price. The bid depth at a given price is the cumulative volume of current buy orders on the book at that price or higher, while the ask depth at a given price is the cumulative volume of current sell orders on the book at that price or lower". Why represent a cumulative volume? The logic behind this is the following: if one is willing to buy 1ETH for 158€, then we assume that he/she is also willing to buy 1ETH for 157€, and so on.