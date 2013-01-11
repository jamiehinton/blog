---
layout: post
title: "custom nuget feed configuration for Azure builds"
date: 2013-01-11 14:31
comments: true
published: true
categories: [Nuget, Azure]
---

When deploying to Azure with Nuget package restore enabled on a solution, you will run into difficulties if you have custom custom Nuget feeds.

By default, Nuget will look at the default feed which at the time of writing is "https://nuget.org/api/v2/".

The problem is that it won't look at your custom feed URL and the build will fail.

To add your custom feed URL open the NuGet.targets file found in the .nuget folder in the root of the solution.

Find the XML node named 'PackageSources' which will be empty. Simple add your custom Nuget feed URL there. 

There are a few little gotchas. It now won't look for the default feed and what is the format for adding multiple feeds?

Firtly the simple answer to it not looking at the default Nuget feed is to just addit to the list and the format for adding multiple feeds is to have each feed in speech marks separated by a semi-colon.

Here is an example:
{% codeblock %}
<PackageSources>"https://nuget.org/api/v2/";"https://custom-nuget-feed.com/nuget"</PackageSources>
{% endcodeblock %}