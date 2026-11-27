---
layout: page
title: publications
permalink: /publications/
description: Deep learning, biomedical signal processing, neuroimaging, medical image analysis, neuromodulation, intelligent biosensing and AI-assisted therapeutic technologies.
nav: true
nav_order: 4
---

{% include brain_style.liquid %}

{% comment %} The list comes from _data/publications.yml. Add new publications there. {% endcomment %}
{% assign pubs = site.data.publications %}
{% assign n_journal = pubs | where: "type", "journal" | size %}
{% assign n_conf = pubs | where: "type", "conference" | size %}
{% assign n_other = pubs.size | minus: n_journal | minus: n_conf %}

<p class="b-lead">Publications by the laboratory's principal investigator and collaborators. For the most up-to-date list, see <a href="https://scholar.google.com/citations?user=xqQrcpYAAAAJ&amp;hl=en" target="_blank" rel="noopener">Google Scholar</a>.</p>

<div class="b-filter" role="group" aria-label="Filter publications"><button class="on" data-f="all">All ({{ pubs.size }})</button><button data-f="journal">Journal articles ({{ n_journal }})</button><button data-f="conference">Conference papers ({{ n_conf }})</button><button data-f="other">Other ({{ n_other }})</button></div>

{% assign years = pubs | group_by: "year" %}
{% for yr in years %}
<div class="b-year"><div class="y">{{ yr.name }}</div><div>
{% for p in yr.items %}{% if p.type == "journal" or p.type == "conference" %}{% assign f = p.type %}{% else %}{% assign f = "other" %}{% endif %}{% case p.type %}{% when "journal" %}{% assign label = "Journal" %}{% when "conference" %}{% assign label = "Conference" %}{% when "data" %}{% assign label = "Data paper" %}{% when "preprint" %}{% assign label = "Preprint" %}{% else %}{% assign label = "PhD thesis" %}{% endcase %}
<div class="b-pub" data-type="{{ f }}"><div class="t">{{ p.title }}</div>{% if p.authors %}<div class="a">{{ p.authors | replace: "Mehmet Akif Özdemir", "<b>Mehmet Akif Özdemir</b>" }}</div>{% endif %}<div class="v"><span class="type {{ f }}">{{ label }}</span><em>{{ p.venue }}</em>{% if p.doi %}<a href="{{ p.doi }}" target="_blank" rel="noopener">DOI</a>{% endif %}{% if p.code %}<a href="{{ p.code }}" target="_blank" rel="noopener">Code</a>{% endif %}{% if p.dataset %}<a href="{{ p.dataset }}" target="_blank" rel="noopener">Dataset</a>{% endif %}</div></div>
{% endfor %}
</div></div>
{% endfor %}

<script>
  document.querySelectorAll(".b-filter button").forEach(function (btn) {
    btn.addEventListener("click", function () {
      var f = btn.dataset.f;
      document.querySelectorAll(".b-filter button").forEach(function (b) { b.classList.toggle("on", b === btn); });
      document.querySelectorAll(".b-pub").forEach(function (p) { p.style.display = (f === "all" || p.dataset.type === f) ? "" : "none"; });
      document.querySelectorAll(".b-year").forEach(function (yr) {
        var any = Array.prototype.some.call(yr.querySelectorAll(".b-pub"), function (p) { return p.style.display !== "none"; });
        yr.style.display = any ? "" : "none";
      });
    });
  });
</script>
