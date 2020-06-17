---
title: "ETHEUR MACD Trading Simulation"
date: 2020-06-14T16:21:50+02:00
draft: true
imagePreview: "/images/etheur-trading-simu-preview.png"
tags: [
    "fintech",
    "D3.js"
]
---

This scrollable graph is generating live simulations of MACD trading.
The initial balance is 100 and the trading fees are 0.26% per trade.

<!--more-->

0.26% is the <a target="_blank" href="https://support.kraken.com/hc/en-us/articles/201893638-How-trading-fees-work-on-Kraken">
Kraken exchange entry level fee</a>

<div class="container">
    <div class="row">
        <div class="col-12">
            <h3 id="titre">Hello</h3>
            <svg></svg>
        </div>
    </div>
</div>

<script src="/script/computeMacdSimulation.js"></script>
<script src = "/script/etheur-trading-simu.js"></script> 
