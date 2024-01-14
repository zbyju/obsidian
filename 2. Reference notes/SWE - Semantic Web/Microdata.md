Microdata is part of the HTML5 specification backed by Google and it includes vocabularies and global attributes.

They are similar to microformats, but:
- items (collection of properties) have ids (URIs)
- Vocabulary has a formal description of terms:
	- schema.org is a standard
- data formats are not directly based on formats (such as vCard, vCalendar) but they define its own vocabulary

Microdata can be specified on any HTML element using:
- itemscope
- itemtype
- itemid
- itemprop
- itemref

```html
<section>
	My name is Peter Brown and I work as a post-doc at the Innsbruck University.
	My friends often call me Pete. My office address is
	Technikestrasse 21a, 6020, Innbruck, and you can also visit my homepage at
	<a href="http://peter-brown.org">http://peter-brown.org</a>
</section>

<section itemscope itemtype="http://schema.org/Person">
	My name is <span itemprop="name">Peter Brown</span> and I work as a
	<span itemprop="title">post-doc</span> at the
	<span itemprop="affiliation">Innsbruck University</span>.
	
	My friends often call me <span itemprop="nickname">Pete</span>.
	
	<section itemprop="address" itemscope itemtype="http://schema.org/Address">
		My office address is 
		<span itemprop="street-address">Technikestrasse 21a</span>
		<span itemprop="postal-code">6020<span>,
		<span itemprop="locality">Innsbruck</span>
	</section>
	and you can also visit my homepage at
	<a href="http://peter-brown.org" itemprop="url">http://peter-brown.org</a>
</section>
```


[[_SWE Reference]]
[[2. Reference notes/SWE - Semantic Web/RDF|RDF]]
[[Web Annotations]]
[[Microformats vs Microdata]]