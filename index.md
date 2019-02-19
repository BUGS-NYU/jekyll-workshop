---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: home
---
A spider web, spiderweb, spider's web, or cobweb (from the archaic word coppe, meaning "spider") is a structure created by a spider out of proteinaceous spider silk extruded from its spinnerets, generally meant to catch its prey.

## Blog
* [January Edits of BUGS Website](/blog/2019/01/january-edits-bugs-site)
* [Incredible Workshop](/blog/2019/02/clearly-the-best-workshop)
* [Style Guide](/blog/2019/02/style-guide-for-bugs-website)

## Classes
{% for class in site.classes %}
* [{{ class.title }}]({{ class.url }}){% endfor %}

## Projects
{% for project in site.projects %}
* [{{ project.title }}]({{ project.url }}){% endfor %}
