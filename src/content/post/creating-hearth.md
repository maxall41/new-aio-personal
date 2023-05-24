---
title: A LavaLink Alternative with 30X Higher Performance
description: Hearth is a LavaLink alternative that has 30x Higher performance
publishDate: "23 May 2023"
tags: ["Software","Discord","Rust"]
---

I recently began working on a high-performance alternative to LavaLink written in Rust. It uses 30X less memory than LavaLink allowing
for more concurrent streams and saving on server costs. 


## Performance
As previously mentioned Hearth uses 30X less memory than LavaLink with the same load. Unfortunately, Its CPU usage is currently slightly higher than LavaLink (but almost equivalent), due to inefficiencies
in `Songbird` the client library Hearth uses to process and stream audio to Discord. But this should be fixed in a future update to Hearth. Which will allow Hearth to provide massive performance gains over LavaLink.

## Client Libraries

Unlike LavaLink, Hearth has native client librarie(s). Currently Charcoal (Client library written in Rust) only supports Rust but bindings are coming soon for Java, Typescript, and Python!

## Features

Hearth does not yet have feature parity with LavaLink, but it does support a basic subset of LavaLink's functionality meaning that it supports everything except:
* Filters
* Analytics
* Event System

But all of these things should be coming soon in a future update!

## Scaling
Hearth is designed from the ground up for massive scale. Based on a scheduler system allows hundreds of worker nodes to be connected. And the great thing about this system is because it uses a message broker instead of HTTP calls, it opens the door for worker nodes to be auto-scaled 🤯. So you don't have to have 20 workers running to service load at 3 am in the morning you only need 2. But at peak hours it can be scaled up with no effort on your part. This is not currently possible, but should be coming soon!

## Conclusion
To get an updated view of the features, and performance improvements mentioned above will be released see our GitHub progress board [here](https://github.com/orgs/Hearth-Industries/projects/1/views/1?layout=board). Additionally Hearth is open-source so if you want to add anything or help out with implementing anything just create a PR, or issue in the repo [here](https://github.com/Hearth-Industries/Hearth)