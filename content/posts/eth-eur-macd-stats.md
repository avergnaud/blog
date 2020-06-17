---
title: "ETHEUR MACD trading statistics"
date: 2020-06-15T17:06:35+02:00
draft: false
imagePreview: "/images/eth-eur-macd-stats-preview.png"
tags: [
    "fintech",
]
---

For every 1 year span of MACD trading on the ETHEUR market, how many simulations:

<ul>
    <li>
        beat the market?
    </li>
    <li>
        make a profit?
    </li>
</ul>

<!--more-->

<a target="_blank" href="/posts/etheur-trading-simu/">
This previous article
</a> provided a visual representation of the MACD trading simulations.

This post shows the overall performance of the MACD trading strategy...

<hr>
<div>
    Market data: From 
    <b><span id="range-from"></span></b>
    to 
    <b><span id="range-to"></span></b>
</div>
<div>
    Number of 1 year span trading simulations: 
    <b><span id="number-sims"></span></b>
</div>
<ul>
    <li>
        <b><span id="result-beat-market"></span></b> beat the market
    </li>
    <li>
        <b><span id="result-make-profit"></span></b> make a profit
    </li>
</ul>

<div class="tableLimited">
    <table class="table table-sm">
        <thead>
            <tr>
            <th scope="col">From</th>
            <th scope="col">To</th>
            <th scope="col">Market Perf</th>
            <th scope="col">Trading Perf</th>
            <th scope="col">Beats the market</th>
            <th scope="col">Makes a profit</th>
            </tr>
        </thead>
        <tbody id="results-tbody">
        </tbody>
    </table>
</div>
<div class="container">
    <div class="row">
        <div class="col-12">
        </div>
    </div>
</div>

<script src="/script/computeMacdSimulation.js"></script>
<script src="/script/eth-eur-macd-stats.js"></script>
