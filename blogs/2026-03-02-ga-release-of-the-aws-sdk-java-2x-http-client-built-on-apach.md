---
title: "GA Release of the AWS SDK Java 2.x HTTP Client built on Apache HttpClient 5.6"
url: "https://aws.amazon.com/blogs/developer/ga-release-of-the-aws-sdk-java-2-x-http-client-built-on-apache-httpclient-5-6/"
date: "Mon, 02 Mar 2026 19:24:38 +0000"
author: "Dongie Agnir"
feed_url: "https://aws.amazon.com/blogs/developer/feed/"
---
<p>If you’re using the Apache HttpClient 4.5.x with the&nbsp;<a href="https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/home.html" rel="noopener noreferrer" target="_blank">AWS SDK for Java 2.x</a>, you may have encountered dependency alerts for Jakarta Commons Logging (JCL) dependencies, concerns about long-term maintenance support, or compatibility issues with Java 21’s virtual threads. The new Apache 5 HTTP client solves these problems.</p> 
<p>In this post, you’ll learn how to add the Apache 5 HTTP client to your project, configure it for your needs, and migrate from the 4.5.x version.</p> 
<h3>What’s new</h3> 
<ul> 
 <li><strong>Modern logging</strong>: Replaces the outdated JCL dependency with Simple Logging Facade for Java (SLF4J), giving you better compatibility with modern logging frameworks like Logback and Log4j2</li> 
 <li><strong>Virtual thread support</strong>: Full compatibility with Java 21’s virtual threads for improved concurrency</li> 
 <li><strong>Active maintenance</strong>: Apache HttpClient 5.x receives regular security updates and bug fixes</li> 
</ul> 
<p>This client is available alongside the existing SDK HTTP clients: Apache HttpClient 4.5.x, Netty, URL Connection, and AWS CRT HTTP client. The new&nbsp;apache5-client&nbsp;Maven artifact lets you use both Apache versions in the same project without conflicts.</p> 
<h2>Getting started</h2> 
<p>Using the Apache 5 HTTP client in your SDK can require as little as a single step. If you’re coming from the Apache 4 client and want to set specific configurations, the new Apache 5 client offers identical options.</p> 
<h3>Add the Apache 5&nbsp;client dependency</h3> 
<p>To begin using the&nbsp;Apache 5 HTTP client implementation, add the following dependency to your project:</p> 
<div class="hide-language"> 
 <pre><code class="lang-html">&lt;dependency&gt;
&nbsp;&nbsp; &nbsp;&lt;groupId&gt;software.amazon.awssdk&lt;/groupId&gt;
&nbsp;&nbsp; &nbsp;&lt;artifactId&gt;apache5-client&lt;/artifactId&gt;
&nbsp;&nbsp; &nbsp;&lt;version&gt;2.41.26&lt;/version&gt;
&lt;/dependency&gt;</code></pre> 
</div> 
<p>If you just want to use all the default configurations, then you do not need to configure anything else; your sync clients will use the Apache5 client under the hood.</p> 
<p><code>S3Client s3Client = S3Client.create();</code></p> 
<p><strong>Advanced configuration example</strong></p> 
<p>If you want to configure certain options on the client, then just like with all of our clients, you can use&nbsp;<code>Apache5HttpClient.builder()</code>&nbsp;to obtain a builder and set the options you would like to:</p> 
<div class="hide-language"> 
 <pre><code class="lang-java">Apache5HttpClient httpClient = Apache5HttpClient.builder()
&nbsp;&nbsp; &nbsp;.connectionTimeout(Duration.ofSeconds(30))
&nbsp;&nbsp; &nbsp;.maxConnections(100)
&nbsp;&nbsp; &nbsp;.build();

DynamoDbClient dynamoDbClient = DynamoDbClient.builder()
&nbsp;&nbsp; &nbsp;.httpClient(httpClient)
&nbsp;&nbsp; &nbsp;.build();</code></pre> 
</div> 
<h3>Migrate from Apache 4.5.x</h3> 
<p>If you’re using the default Apache HTTP client, migration is straightforward:</p> 
<ol> 
 <li>Add the&nbsp;apache5-client&nbsp;dependency shown above</li> 
 <li>Update any explicit&nbsp;ApacheHttpClient&nbsp;references to&nbsp;Apache5HttpClient</li> 
</ol> 
<p>The API remains consistent with other HTTP client implementations in the SDK. Note that like the 4.5.x client, this implementation supports synchronous service clients only.</p> 
<p><strong>Cleaning up</strong></p> 
<p>When you’re done with a service client, close it to release resources:</p> 
<div class="hide-language"> 
 <pre><code class="lang-java">
s3Client.close();
</code></pre> 
</div> 
<p>If you created a shared&nbsp;Apache5HttpClient&nbsp;instance, close it separately after closing the service clients that use it.</p> 
<h3>Conclusion</h3> 
<p>In this blog post, we showed you how to get started with the new Apache 5 HTTP client in the AWS SDK for Java 2.x, which uses Apache HttpClient 5.6.x. Please share your experience and any feature requests by opening a <a href="https://github.com/aws/aws-sdk-java-v2/issues" rel="noopener noreferrer" target="_blank">GitHub issue</a>.</p> 
<hr style="width: 80%;" />
