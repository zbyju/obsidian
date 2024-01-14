They try to solve embedding data into HTML, XHTML, Atom, XML. Browsers still display HTML, machines process data from microformats.

There are some core principles to microformats:
- Use semantic HTML elements
	- nav, main, section, article, ...
	- otherwise you need to settle for div, span

# class-design-pattern
Semantic meaning is indicated on HTML using class attribute:
```html
<div class="vcard">
	<a class="url fn" href="http://www.vitvar.com">Tomas Vitvar</a>,
	<span class="org">UIBK&lt;/span>
</div>
```
=> For example by using vcard.

# value-class-pattern
We can embed data structure when a property has subproperties (telephone = type + number)