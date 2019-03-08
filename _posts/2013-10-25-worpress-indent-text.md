---
id: 40
title: Worpress indent text
date: 2013-10-25T02:54:21+00:00
author: rpbaltazar
layout: post
guid: http://balazar.net/random/?p=40
permalink: /2013/10/25/worpress-indent-text/
categories:
  - Blogging
tags:
  - html
  - indentation
  - wordpress
---
The problem:  
I have a piece of code that I want to show indented, but adding blank spaces by pressing the space bar is not solving the issue.

Also, using &#8220;&nbsp;&#8221; will disappear if I jump from Visual to Text mode.

The solution:

  * <pre>Use this html trick: &lt;span style="visibility: hidden;"&gt;+++&lt;/span&gt;</pre>
    
    The number of characters give you the indentation. The character used is not important.</li> 
    
      * <pre>Single line indentation is also possible by using the following: &lt;span style="margin-left:28px;"&gt;Start writing here&lt;/span&gt;</pre></ul> 
    
    <a href="http://wpbtips.wordpress.com/2009/06/19/formatting-text-pt-2/" target="_blank">Full reference</a>