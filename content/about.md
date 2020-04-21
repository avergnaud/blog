---
date: 2020-04-20
type: section
title: "About"
---

Personal blog detailing the sources on [https://github.com/avergnaud](https://github.com/avergnaud)

<div id="languages-result">Loading repositories...</div>

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

        var listDiv = document.getElementById("languages-result");
        listDiv.innerHTML = ''
        for (s of sortable) {
        if (s[0] != "null") {
            // do stuff
            var languageDiv = document.createElement('div');
            var lien = "<a href='https://github.com/search?q=user%3Aavergnaud+language%3A" 
                        + s[0] 
                        + "&s=updated' target='_blank'>" 
                        + s[0] 
                        + "</a>"
            languageDiv.innerHTML = lien + ' <span class="rnb">' + s[1] + '</span>';  
            listDiv.appendChild(languageDiv);
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
