---
layout: posts
title:  "Thoughts on Abandoned Projects"
date:   2020-09-25
categories: personalThoughts
---

I recently worked with a team where they needed to combine data currently available from their Power BI reports with additional data in a separate process ending in a SQL database. Going back to the same data sources was possible, but there were a large number of transformations and measures within Power BI they would need to replicate.

Fortunately, Power BI has made the XMLA endpoints for the underlying analysis services database available for querying. On the transfer side, the team was already using Data Factory to move data into their database. The problem is, there is no connector between Data Factory and Analysis Services or Power BI. What it does have, is the ability to create a custom connector via an Azure Function.