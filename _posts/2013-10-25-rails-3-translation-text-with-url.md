---
id: 32
title: Rails 3++ translation text with url
date: 2013-10-25T02:27:44+00:00
author: rpbaltazar
# layout: post
guid: http://balazar.net/random/?p=32
permalink: /2013/10/25/rails-3-translation-text-with-url/
categories:
  - Computer Science
tags:
  - internationalization
  - rails 3
  - rails 4
  - ror
  - translation
  - YAML
---
Problem:
I want to have a link in the translation file. The text associated with the link also has to be translatable.

My YAML file with english version:
`<br />
...<br />
messages:<br />
<span style="visibility: hidden;">++</span>surveyclosed: "If you have any issues or questions, please contact us through our email or phone number available in %{contacts_url} page"<br />
<span style="visibility: hidden;">++</span>surveyclosed_link: "contacts"<br />
`

This results in

<pre>If you have any issues or questions, please contact us through our email or phone number available in &lt;a href="/contacts"&gt;contacts&lt;/a&gt; page</pre>

The reason:
Rails 3 automatically escapes the translation file.

The solution:
suffix the YAML translation tag with _html. This way, Rails won&#8217;t escape the translation and put the link correctly

`<br />
...<br />
messages:<br />
<span style="visibility: hidden;">++</span>surveyclosed_html: "If you have any issues or questions, please contact us through our email or phone number available in %{contacts_url} page"<br />
<span style="visibility: hidden;">++</span>surveyclosed_link: "contacts"<br />
`
