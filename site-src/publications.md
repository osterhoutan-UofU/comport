---
layout: page
title: Publications
---

<div id="collapsible-bib">
</div>

<div id="collapsible-bib-gen">

{% bibliography %}

</div>

<!-- !! THIS MUST BE INCLUDED IN ANY FILE THAT CALLS `{{ bibliography }}` !! -->
<script type="text/javascript">
    // - Add pertinent css ----
    var styles = `
    /* COLLAPSIBLE ITEM STUFF */

    /* Style the button that is used to open and close the collapsible content */
    .collapsible-bib-btn {
        background-color: #4B6C86;
        color: white;
        cursor: pointer;
        padding: 18px;
        width: 100%;
        border: none;
        text-align: left;
        outline: none;
        font-size: 15px;
    }

    /* Add a background color to the button if it is clicked on (add the .active class with JS), and when you move the mouse over it (hover) */
    .collapsible-bib-btn:hover {
        background-color: #ccc;
    }

    .collapsible-bib-active {
        background-color: #204765;
    }

    /* Style the collapsible content. Note: hidden by default */
    .collapsible-bib-content {
        padding: 0 18px;
        display: none;
        overflow: hidden;
        background-color: #5d7a9151;
        color: black;
        max-height: 0;
        transition: max-height 0.2s ease-out;
    }

    /* Add icon  */
    .collapsible-bib-btn:after {
        content: url({{ "/images/cite.svg" | absolute_url }});
        color: white;
        float: right;
        margin-left: 5px;
        fill: none;
        -webkit-transition: -webkit-transform 1s ease-in-out;
        -ms-transition: -ms-transform 1s ease-in-out;
        transition: transform 1s ease-in-out;
    }

    .collapsible-bib-active:after,
    .collapsible-bib-btn:hover:after {
        transform: rotate(180deg);
        -ms-transform: rotate(180deg);
        -webkit-transform: rotate(180deg);
    }

    .collapsible-bib-active {
        fill: white;
    }
    `
    var styleSheet = document.createElement("style")
    styleSheet.type = "text/css"
    styleSheet.innerText = styles
    document.head.appendChild(styleSheet)


    // - Extract Bib entries from list ----
    var genDiv = document.getElementById("collapsible-bib-gen");
    var outDiv = document.getElementById("collapsible-bib");
    var all_entries = document.getElementsByClassName("collapsible-bib");
    var headerElements = genDiv.getElementsByTagName("h2");
    
    var headers = [];
    for (var elem of headerElements) {
        headers.push(elem.textContent);
    }
    years.sort();

    for (var y of years) {
        var year_entries = all_entries.getElementsByClassName("collapsible-bib-entry-year-"+y);
        var secDiv = document.createElement("div");
        secDiv.id = "collapsible-bib-section-year-"+y;
        secDiv.classList.push("collapsible-bib-section");
        outDiv.children.appendChild(secDiv);
        var secHeader = document.createElement("h2");
        secHeader.textContent = y;
        outDiv.children.appendChild(secHeader);
        for (var e of year_entries) {
            outDiv.children.appendChild(e);
        }
    }
    genDiv.innerHTML = '';


    // - Modify all pertinent collapsible elements ----
    var coll = document.getElementsByClassName("collapsible-bib-btn");
    var i;

    for (i = 0; i < coll.length; i++) {
        coll[i].addEventListener("click", function () {
            this.classList.toggle("collapsible-bib-active");
            var content = this.nextElementSibling;
            if (content.style.maxHeight) {
                content.style.maxHeight = null;
            } else {
                content.style.maxHeight = content.scrollHeight + "px";
            }
        });
    }
</script> 