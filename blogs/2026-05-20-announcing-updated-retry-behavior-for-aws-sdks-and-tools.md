---
title: "Announcing updated retry behavior for AWS SDKs and Tools"
url: "https://aws.amazon.com/blogs/developer/announcing-updated-retry-behavior-for-aws-sdks-and-tools/"
date: "2026-05-20"
author: "Matthew Miller"
feed_url: "https://aws.amazon.com/blogs/developer/feed/"
---
When your application calls an AWS service and the request fails with a retryable error, the AWS SDK retries it automatically. The retry behavior controls how long the SDK waits between attempts and when it gives up. Most of this happens in the background, but it directly affects how your application experiences errors and latency.
