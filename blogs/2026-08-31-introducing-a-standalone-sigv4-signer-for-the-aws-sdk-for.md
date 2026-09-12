---
title: "Introducing a standalone SigV4 signer for the AWS SDK for .NET"
url: "https://aws.amazon.com/blogs/developer/introducing-a-standalone-sigv4-signer-for-the-aws-sdk-for-net/"
date: "2026-08-31"
author: "Garrett Beatty"
feed_url: "https://aws.amazon.com/blogs/developer/feed/"
---
Until now, signing an AWS request that no generated SDK client covered meant reaching into internal SDK types or hand-writing the AWS Signature Version 4 (SigV4) algorithm. The AWS SDK for .NET now includes a public SigV4 signer you can call directly. Use the signer to add SigV4 authentication to an HTTP request, or to […]
