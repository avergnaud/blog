---
date: 2020-04-20
type: section
title: "About"
---

This is my personal blog providing details about the projects on [https://github.com/avergnaud](https://github.com/avergnaud)

<div id="loading">Loading repositories...</div>
<table id="languages-result">
<tr>
    <th>Language</th>
    <th>repositories</th>
  </tr>
</table>

<script>

    var mapper = function(ent){return ent.language},
    reducer = function(stats, lang) {stats[lang] = (stats[lang] || 0) + 1; return stats};
  
    window.ghApiCallHandler = function(result) {
    if (Math.floor(result.meta.status/100) == 2) {
        langStats = result.data.map(mapper).reduce(reducer, {});

        var sortable = [];
        for (var language in langStats) {
            sortable.push([language, langStats[language]]);
        }
        sortable.sort(function(a, b) {
            return b[1] - a[1];
        });

        var table = document.getElementById("languages-result");
        document.getElementById("loading").innerHTML = '';
        for (s of sortable) {
            if (s[0] != "null") {
                // do stuff
                var languageRow = document.createElement('tr');
                var lien = "<a href='https://github.com/search?q=user%3Aavergnaud+language%3A" 
                            + s[0] 
                            + "&s=updated' target='_blank'>" 
                            + s[0] 
                            + "</a>";
                var lienCell = document.createElement('td');
                lienCell.innerHTML = lien;
                languageRow.appendChild(lienCell);
                var nb = "<a href='https://github.com/search?q=user%3Aavergnaud+language%3A" 
                            + s[0] 
                            + "&s=updated' target='_blank'>" 
                            + s[1] 
                            + "</a>";
                var nbCell = document.createElement('td');
                nbCell.innerHTML = nb;
                languageRow.appendChild(nbCell);
                //languageRow.innerHTML = lien + ' <span class="rnb">' + s[1] + '</span>';  
                table.appendChild(languageRow);
            }
        }
    }
    else {
        console.log('Request failed with code ' + result.meta.status);
    }
    };

    window.ghApiCall = function(user) {
    var scrElm = document.createElement('script');
    scrElm.src = 'https://api.github.com/users/' + encodeURI(user) + '/repos?callback=ghApiCallHandler&per_page=100';
    (document.head || document.getElementsByTagName('head')[0]).appendChild(scrElm);
    };

    ghApiCall('avergnaud');
</script>
