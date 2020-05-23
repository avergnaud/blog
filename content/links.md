---
date: 2020-05-22
type: section
title: "Links"
---

### External links

<div>
  <ul>
    <li>
      <img class="icone" src="/images/baeldung_favicon-16x16.png">
      <a target="_blank" href="https://www.baeldung.com/">https://www.baeldung.com/</a>
    </li>
    <li>
      <img class="icone" src="/images/infoq_favicon-16x16.ico">
      <a target="_blank" href="https://www.infoq.com/">https://www.infoq.com/</a>
    </li>
    <li>
      <img class="icone" src="/images/dzone_favicon-16x16.png">
      <a target="_blank" href="https://dzone.com/">https://dzone.com/</a>
    </li>
  </ul>
</div>

<div>
  <p>
    Latest articles from 
      <span style="white-space: nowrap;">
        <img class="icone" src="/images/fowler_favicon-16x16.ico"><a target="_blank" href="https://martinfowler.com/">https://martinfowler.com/</a>:
      </span>
  </p>
  <ul id="martinfowler-articles">
  </ul>
</div>

<script>
  const ul = document.getElementById('martinfowler-articles');
  fetch('https://rss-prxy.herokuapp.com/rss/martinfowler.com')
    .then(response => response.json())
    .then(data => {
      /* json response */
      let items = data.items;
      items.sort(function(a, b) {
              return b['pubDate'] - a['pubDate'];
          });
      items.forEach(item => {
        /* for each item */
        let formattedDate = item.pubDate.substring(0, item.pubDate.indexOf("T"));
        let li = document.createElement('li');
        let lien = "<a href='" + item.link + "'" 
                              + " target='_blank'>" 
                              + item.title
                              + "</a> (" + formattedDate + ")";
        li.innerHTML = lien;
        ul.appendChild(li);
      });
    });
</script>