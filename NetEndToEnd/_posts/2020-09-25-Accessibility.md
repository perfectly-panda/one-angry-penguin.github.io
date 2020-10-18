---
layout: posts
title:  "Accessibility Namespace"
date:   2020-09-25
---

First Accessed: 9/25/2020
Last Update: 9/25/2020
(Definition)[https://docs.microsoft.com/en-us/dotnet/api/accessibility?view=netcore-3.1]: "The Accessibility namespace and all of its exposed members are part of a managed wrapper for the Component Object Model (COM) accessibility interface." 

Of course the first thing on the list would be one I don't normally deal with since this is primarily for desktop applications. The key piece of this namespace is the `IAccessible` interface which helps Windows accessibility tools like screen readers interact with the application. The interface definition includes methods that the accessibility tool can use to help describe and navigate the application.

