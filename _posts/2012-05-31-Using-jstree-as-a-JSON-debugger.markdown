---
layout: post
title: Using jstree as a JSON-debugger
---

I was playing around with the geonames-services, and since they all return JSON-objects,
I thought it'd be nice to show the results of the different services using a html-tree structure.

In javascript, it is really easy to traverse an object:

	var obj = { name: 'Thomas' };

	for (var key in obj) {
		alert( key + ": " + obj[key] );
	}

This code will display an alert with the text "name: Thomas"

jstree
------

jstree (http://www.jstree.com) is a nice		
