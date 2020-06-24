---
title: "ETHEUR MACD Trading Simulation"
date: 2020-06-14T16:21:50+02:00
draft: false
imagePreview: "/images/etheur-trading-simu-preview.png"
tags: [
    "fintech",
    "D3.js"
]
---

This scrollable graph is generating live simulations of MACD trading.
The initial balance is <b>100</b> (fiat) and the trading fees are <b>0.26%</b> per trade.

<!--more-->

<a target="_blank" href="/posts/ohlc-macd-span/">
This previous article
</a> detailled the MACD indicator and the related trading strategy.

This post provides a series of trading simulations. The trading strategy is simple:
<ul>
    <li>Buy the most possible at every buy signal</li>
    <li>Sell everything at every sell signal</li>
</ul>

<b>0.26%</b> is the <a target="_blank" href="https://support.kraken.com/hc/en-us/articles/201893638-How-trading-fees-work-on-Kraken">
Kraken exchange entry level fee</a>

<hr>

<div class="container">
    <div class="row">
        <div class="col-12">
            <h3 id="titre">Hello</h3>
            <svg></svg>
        </div>
    </div>
    <div class="row">
        <div class="col-12">
            <h3>Détail</h3>
            <ul id="detail-list">
            </ul>
        </div>
    </div>
</div>

<script src="/script/computeMacdSimulation.js"></script>
<script src = "/script/etheur-trading-simu.js"></script> 
