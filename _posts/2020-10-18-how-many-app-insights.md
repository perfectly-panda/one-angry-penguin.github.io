---
layout: posts
title:  How Many App Insights Instances Do I Need?
date:   2020-10-18
category: common questions
tags: azure application-insights
---

There are a few questions that I get over and over again. "How many App Insights workspaces do I need?" is one of them. The short answer is "As many as makes sense for your environment." but that doesn't really explain how to determine how to tackle the issue. Fortunately, there are some guidelines to help.

> Note: It's worth keeping in mind that you can join across workspaces, up to 100 max. Using too few workspaces will make the built-in metrics hard to use. Too many can make those same metrics more fragmented than is ideal, but you can pull the data together yourself using joins. Dependency tracking is a bit of an exception here- App Insights will try to join data based on dependencies automatically.

A straightforward way to deal with this is to start with everything you want to monitor in one group, and then divide it up where needed.

## Divide By System/Application
Theoretically you could throw all your data into a single instance and be done with it, but since you are paying by the GB, there's not much financial advantage to doing this. Instead, the first grouping should by application. That means that even if your website's front end and API are hosted separately, you would normally combine them into a single App Insights instance. One the other hand, your external and intranet sites are something you should consider separating unless they share an API.

## Divide By Environment
Put dev, test, and prod into separate instances. It's just so much easier since you'll rarely want to combine the data and combining them would make most of the built-in metrics useless. There might be a reason to combine them, but I can't think of one that would be more advantageous than the disadvantages.

## Divide by Data Retention Settings
Settings like data retention are applied for all the data in that instance. Since you have to pay for storage past the standard 30 days, just pushing all your data into an instance with extended data retention or that pushes data into Storage isn't always the best choice. Instead, use separate instances and join the data when needed.

## Divide by Billing & Security Concerns
If one part of your business has an app that accesses an API owned by another part, you may not want the team that owns the API to pay for the ingestion and storage used by the other business unit. At a higher level, subscriptions can be used to separate billing, and you may wish to split the data into separate instances so that they can be billed separately.

As a similar idea to billing and data retention is security. Anyone with read access to the data will be able to read all data. Keeping PII out of your logging data is a start, but there still may be certain parts of your logs that you want to restrict access to. To accomplish this you will need to split data into different instances.