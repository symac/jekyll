---
title: Index des leçons
layout: blank
permalink: /fr/lecons/
---


# Index

Nos leçons sont organisées en fonction des différentes étapes de recherche et aussi selon de grandes thémtiques. Utilisez les boutons ci-dessous pour filtrer les leçons par catégories. Si vous ne trouvez pas l'outil ou le sujet qui vous intéresse, [contactez-nous]({{site.baseurl}}/feedback).

{% comment %}
See documentation on the use of alllessons and lesson-index in /lessons.md
{% endcomment %}

{% assign alllessons = site.pages | where: "translated-lesson" , "true" | where: "lang" , "fr" %}

{% include lesson-index.html %}