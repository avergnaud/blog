---
title: "OHLC MACD chart"
date: 2020-05-03T10:55:48+02:00
draft: false
imagePreview: "/images/ohlc-macd-span-preview.png"
tags: [
    "fintech",
    "Spring",
    "D3.js",
    "React"
]
---

OHLC chart and MACD indicator for ETHEUR 1day Kraken market data.

See the [demo](https://macd-front.web.app/) hosted on Firebase.

<!--more-->

The graph enables horizontal scrolling. Click the graph to display each period's closing price.

<hr class="ohlc-macd-chart-sep">
<div id="ohlc-macd-chart-price"></div>
<div class="container">
  <div class="row">
    <div class="col-12 col-xl-9">
      <div id="ohlc-macd-chart-area"></div>
    <div>
  </div>
</div>

<hr class="ohlc-macd-chart-sep">

Sources are available on github for the [backend server](https://github.com/avergnaud/macd-definition) and the [ReactJS frontend](https://github.com/avergnaud/macd-front). The Java server is hosted on Heroku and uses a PostgreSQL database. The server requests the Kraken API every two minutes to retrieve the latest OHLC data. It also computes the MACD every two minutes. The ReactJS frontend is hosted on Firebase.

From [wikipedia](https://en.wikipedia.org/wiki/MACD): the MACD, short for moving average convergence/divergence, is a trading indicator used in technical analysis of stock prices. 

As stated by 
<a target="_blank" href="https://en.wikipedia.org/wiki/MACD">wikipedia</a>
, the trading strategy relies on the Signal-ligne crossovers:
A "signal-line crossover" occurs when the MACD and Signal lines cross. The standard interpretation of such an event is a recommendation to buy if the MACD line crosses up through the average line (a "bullish" crossover), or to sell if it crosses down through the average line (a "bearish" crossover). These events are taken as indications that the trend in the stock is about to accelerate in the direction of the crossover. 

<script src = "/script/ohlc-macd-span.js"></script> 
<script>
    const chart = new MacdChart({
      element: document.querySelector('#ohlc-macd-chart-area'),
      config: {
        innerWidth: 435,
        innerOhlcHeight: 167,
        innerMacdHeight: 100,
        margin: {
          top: 50,
          right: 50,
          bottom: 50,
          left: 0,
          xaxis: 50,
          yaxis: 50
        },
        timeFormat: "%Y-%m-%d"
      }
    });
    Promise.all([
      d3.json("https://macd-definition.herokuapp.com/ohlc/?chartEntityId=2&last=100"),
      d3.json("https://macd-definition.herokuapp.com/macd/?macdDefinitionId=1&last=100"),
      /*
      d3.json("http://localhost:8080/ohlc/?chartEntityId=9395"),
      d3.json("http://localhost:8080/macd/?macdDefinitionId=9394"),
      */
    ]).then(function (data) {
      const macdByTimestamp = new Map();
      data[1].forEach(item => {
        macdByTimestamp.set(item.timeEpochTimestamp, {
          macdValue: item.macdValue,
          signalValue: item.signalValue
        });
      });
      let ohlcData = data[0];
      let formattedData = ohlcData.map(item => {
        let macdObj = macdByTimestamp.get(item.timeEpochTimestamp);
        return {
            timeStamp: item.timeEpochTimestamp * 1000,
            time: new Date(item.timeEpochTimestamp * 1000),
            open: item.openingPrice,
            high: item.highPrice,
            low: item.lowPrice,
            close: item.closingPrice,
            macd: macdObj ? macdObj.macdValue : undefined,
            signal: macdObj ? macdObj.signalValue : undefined
        }});
      chart.draw(formattedData);
    });
  </script>