---
title: "Introducing multipart download support for AWS Tools for PowerShell v5"
url: "https://aws.amazon.com/blogs/developer/introducing-multipart-download-support-for-aws-tools-for-powershell-v5/"
date: "2026-06-01"
author: "Sanket Tangade"
feed_url: "https://aws.amazon.com/blogs/developer/feed/"
---
The new multipart download support in AWS Tools for PowerShell v5 improves the performance of downloading large objects from Amazon Simple Storage Service (Amazon S3) compared to the single-stream downloads. The Read-S3Object and Copy-S3Object cmdlets now deliver faster download speeds through an opt-in switch parameter -UseMultipartDownload for multipart downloads, reducing the need for complex code to manage […]
