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
We can embed data structure when a property has subproperties (telephone = type + number).
```html
<span class="tel">
	<span class="type">Work</span>:
	<span class="value">+43 554 554 556</span>
</span>
```

# include-pattern
We can use this to include a subset of some data from one area of a page (the same page) to another. We can do this using class `include`.

```html
<div class="vcard" id="uibk-card">
	<div class="fn org">University of Innsbruck</div>
		<div class="adr">
			<span class="street-address">Technikestrasse 21a</span>,
			<span class="locality">Tirol</span>
			<span class="postal-code">6020</span>
		</div>
	</div>
</div>

<div class="hreview">
	<h1 class="summary">A place to study computer science!</h1>
	<div class="item">
		<a class="include" href="#uibk-card">Innsbruck Uni</a>
		<p class="description">Courses in English, fields of computer science.</p>
	</div>
</div>
```

# Known issues
- Name conflicts
	- More microformats on the same page can cause conflicts
- Scalability
	- Again leads to conflicts
- No formal semantic, no reasoning support
	- There is a lack of compatibility with other technologies (RDF/RDFa)


[[2. Reference notes/SWE - Semantic Web/RDF|RDF]]
[[Web Annotations]]