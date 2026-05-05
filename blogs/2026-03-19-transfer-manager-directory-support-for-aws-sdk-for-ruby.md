---
title: "Transfer Manager Directory Support for AWS SDK for Ruby"
url: "https://aws.amazon.com/blogs/developer/transfer-manager-directory-support-for-aws-sdk-for-ruby/"
date: "Thu, 19 Mar 2026 14:39:01 +0000"
author: "Juli Tera"
feed_url: "https://aws.amazon.com/blogs/developer/feed/"
---
<p>Managing bulk file transfer to <a href="https://aws.amazon.com/s3/" rel="noopener noreferrer" target="_blank">Amazon Simple Storage Service (Amazon S3)</a> can be complex when transferring directories containing multiple files and subdirectories. <a href="https://aws.amazon.com/sdk-for-ruby/" rel="noopener noreferrer" target="_blank">AWS SDK for Ruby</a> Transfer Manager (<code>aws-sdk-s3</code> version 1.215) now supports directory upload and download. This feature can help streamline bulk transfers by providing multipart handling and parallelism options.</p> 
<p>Previously, uploading directories to Amazon S3 required manual iteration and handling. You also had to manage multipart uploads for large files and implement parallelism for performance. With directory support in Transfer Manager, you can handle this with a single method call that automates the process. In this post, we show you how to upload and download directories using Transfer Manager, customize transfer with filtering options and handle results effectively.</p> 
<h2>Getting started</h2> 
<p>This support requires <code>aws-sdk-s3</code> version&nbsp;1.215 or higher. Add <code>aws-sdk-s3</code>&nbsp;to your Gemfile:</p> 
<pre><code class="lang-ruby">gem 'aws-sdk-s3', '&gt;= 1.215'</code></pre> 
<h3>Initialize the Transfer Manager</h3> 
<p>To initialize a Transfer Manager with a default S3 client:</p> 
<pre><code class="lang-ruby">require 'aws-sdk-s3' 
tm = Aws::S3::TransferManager.new</code></pre> 
<p>Or you could create a custom S3 client to pass to the Transfer Manager.</p> 
<pre><code class="lang-ruby">client = Aws::S3::Client.new(region: 'us-east-1')
tm = Aws::S3::TransferManager.new(client: client)</code></pre> 
<h3>Upload a directory</h3> 
<p>Upload a local directory to an S3 bucket by providing a source path and bucket name:</p> 
<pre><code class="lang-ruby">tm.upload_directory('/path/to/directory', bucket: 'my-bucket')</code></pre> 
<p>By default, only files in the specified directory are uploaded. To include subdirectories, set&nbsp;<code>recursive: true</code>:</p> 
<pre><code class="lang-ruby">tm.upload_directory('/path/to/directory', bucket: 'my-bucket', recursive: true)</code></pre> 
<h3>Download a directory</h3> 
<p>Download objects from an S3 bucket to a local directory by providing a destination path and bucket name:</p> 
<pre><code class="lang-ruby">tm.download_directory('/local/path', bucket: 'my-bucket')</code></pre> 
<p>To download only objects with a specific prefix, set <code>s3_prefix</code>. The full object key is preserved in the local path. For example, given <code>s3_prefix: 'photos/'</code>:</p> 
<ul> 
 <li>Object key: <code>photos/vacation/beach.jpg</code></li> 
 <li>Resolved local path: <code>/local/path/photos/vacation/beach.jpg</code></li> 
</ul> 
<pre><code class="lang-ruby">tm.download_directory('/local/path', bucket: 'my-bucket', s3_prefix: 'photos/2026/')</code></pre> 
<h3>Filtering contents</h3> 
<p>You can also filter transfers by using <code>filter_callback</code>:</p> 
<pre><code class="lang-ruby"># Upload only .txt files 
filter = proc { |_path, name| name.end_with?('.txt') } 
tm.upload_directory('/path/to/directory', bucket: 'my-bucket', filter_callback: filter) 

# Download only .jpg files 
filter = proc { |obj| obj.key.end_with?('.jpg') } 
tm.download_directory('/local/path', bucket: 'my-bucket', filter_callback: filter)</code></pre> 
<h3>Handling results</h3> 
<p>On success, both operations return a hash containing completed and failed transfer details:</p> 
<pre><code class="lang-ruby">result = tm.upload_directory('/path/to/directory', bucket: 'my-bucket') 
# =&gt; { completed_uploads: 7, failed_uploads: 0 }</code></pre> 
<p>By default, an error raises an exception, which stops the transfer but does not clean up completed transfers. You can set <code>ignore_failure: true</code>&nbsp;to continue transferring remaining files and see what errors occurred in the results hash.</p> 
<pre><code class="lang-ruby">result = tm.upload_directory(
  '/path/to/directory', 
  bucket: 'my-bucket', 
  ignore_failure: true
)
# =&gt; { completed_uploads: 5, failed_uploads: 2, errors: [...] }</code></pre> 
<h2>Conclusion</h2> 
<p>Directory upload and download support in the AWS SDK for Ruby Transfer Manager can help streamline bulk S3 transfers with built-in parallelism and multipart handling.</p> 
<p><strong>Key takeaways:</strong></p> 
<ul> 
 <li>Use <a href="https://docs.aws.amazon.com/sdk-for-ruby/v3/api/Aws/S3/TransferManager.html#upload_directory-instance_method" rel="noopener noreferrer" target="_blank"><code>upload_directory</code></a> and <a href="https://docs.aws.amazon.com/sdk-for-ruby/v3/api/Aws/S3/TransferManager.html#download_directory-instance_method" rel="noopener noreferrer" target="_blank"><code>download_directory</code></a> for bulk transfers with a single method call</li> 
 <li>Customize behavior with options like <code>recursive</code>, <code>s3_prefix</code>, and <code>filter_callback</code></li> 
 <li>Handle errors gracefully with <code>ignore_failure</code> and inspect results for details</li> 
</ul> 
<p>These are only a few of the available options. See the <a href="https://docs.aws.amazon.com/sdk-for-ruby/v3/api/Aws/S3/TransferManager.html" rel="noopener noreferrer" target="_blank">API documentation</a> for a full list.</p> 
<p><strong>Next steps:</strong>&nbsp;Try implementing directory transfers in your applications and explore other Transfer Manager features like <a href="https://docs.aws.amazon.com/sdk-for-ruby/v3/api/Aws/S3/TransferManager.html#upload_file-instance_method" rel="noopener noreferrer" target="_blank"><code>upload_file</code></a> and&nbsp;<a href="https://docs.aws.amazon.com/sdk-for-ruby/v3/api/Aws/S3/TransferManager.html#download_file-instance_method" rel="noopener noreferrer" target="_blank"><code>download_file</code></a> for single-object transfers.</p> 
<p>Share your questions, comments, and issues with us on <a href="https://github.com/aws/aws-sdk-ruby" rel="noopener noreferrer" target="_blank">GitHub</a>.</p> 
<hr /> 
<h2>About the author</h2>
