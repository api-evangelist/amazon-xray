---
title: "Announcing response streaming for .NET on AWS Lambda"
url: "https://aws.amazon.com/blogs/developer/announcing-response-streaming-for-net-on-aws-lambda/"
date: "2026-08-05"
author: "Norm Johanson"
feed_url: "https://aws.amazon.com/blogs/developer/feed/"
---
Today, we are announcing support for AWS Lambda response streaming for .NET Lambda functions. With response streaming, functions can be more responsive by sending data back to the caller incrementally as it becomes available, rather than buffering the entire response in memory before returning it. Why response streaming?
