---
title: "Create minimal reproductions for AWS SDK JavaScript v3 with create-aws-sdk-repro"
url: "https://aws.amazon.com/blogs/developer/create-minimal-reproductions-for-aws-sdk-javascript-v3-with-create-aws-sdk-repro/"
date: "Thu, 23 Apr 2026 18:37:18 +0000"
author: "John Lwin"
feed_url: "https://aws.amazon.com/blogs/developer/feed/"
---
<p>We’re excited to announce <a href="https://github.com/awslabs/create-aws-sdk-repro" rel="noopener noreferrer" target="_blank">create-aws-sdk-repro</a>, an open source tool that generates ready-to-run <a href="https://aws.amazon.com/sdk-for-javascript/" rel="noopener" target="_blank">AWS SDK for JavaScript</a> v3 projects.</p> 
<p>You answer a few prompts, pick a service, an operation, environment, and the tool generates a project with everything wired up. With AWS credentials configured, it’s ready to run. In this post, we walk through how the tool works, what it generates, and how to use it.</p> 
<h2>Use cases</h2> 
<h3>Getting started with a new service</h3> 
<p>Instead of piecing together documentation and examples, generate a working project for any AWS service in seconds. The correct imports, credential handling, and error handling are already in place.</p> 
<h3>Testing SDK behavior</h3> 
<p>Quickly spin up isolated projects to test specific SDK operations without affecting your main codebase.</p> 
<h3>Troubleshooting SDK issues</h3> 
<p>If you run into an SDK issue, generate a minimal repro with your service and operation, run it, and share the output in your GitHub issue. A clean project without framework dependencies makes it easier to isolate the problem and get to a resolution faster.</p> 
<h2>Walkthrough</h2> 
<p>In this walkthrough, you will generate a Node.js project that calls the Amazon S3 ListBuckets operation in the us-west-2 AWS Region. Each step shows which option to select so you can follow along.</p> 
<h3>Prerequisites</h3> 
<ul> 
 <li>Install Node.js version 20 or later. See <a href="https://nodejs.org/en/download" rel="noopener noreferrer" target="_blank">Node.js downloads</a> for instructions.</li> 
 <li>For Node.js projects, configure AWS credentials by running aws configure. For more information, see Configuring the <a href="https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/configuring-the-jssdk.html" rel="noopener noreferrer" target="_blank">AWS SDK for JavaScript</a>.</li> 
 <li>For Browser and React Native projects, set up an Amazon Cognito identity pools. The tool generates a <code>COGNITO_SETUP.md</code> guide with step-by-step instructions. For more information, see <a href="https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-identity.html" rel="noopener noreferrer" target="_blank">Amazon Cognito identity pools</a>.</li> 
</ul> 
<h5>Step 1: Run the CLI</h5> 
<pre><code class="lang-bash">$ npm create @aws-sdk/repro</code></pre> 
<h5>Step 2: Select your environment</h5> 
<p>The CLI prompts for the JavaScript environment:</p> 
<pre><code class="lang-bash">? Select JavaScript environment: › - Use arrow-keys. Return to submit.
❯   Node.js
    Browser
    React Native</code></pre> 
<p>Node.js uses the default <a href="https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/setting-credentials-node.html" rel="noopener noreferrer" target="_blank">AWS credentials chain</a>. Browser generates a Vite-based project with <a href="https://aws.amazon.com/cognito/" rel="noopener noreferrer" target="_blank">Amazon Cognito</a> identity pools for browser-safe credentials. React Native creates a full native project with required polyfills.</p> 
<h5>Step 3: Enter a project name</h5> 
<pre><code class="lang-bash">? Enter project name: aws-sdk-repro-a1b2c3d4</code></pre> 
<p>The tool suggests a default name with the prefix <code>aws-sdk-repro-</code> followed by a random identifier for uniqueness. You can enter a custom name. The name must be non-empty and cannot contain the characters <code>/ \ : * ? " &lt; &gt; |</code>&nbsp;or path traversal sequences (<code>..</code>). For React Native projects, the name is further sanitized to alphanumeric characters only. For this walkthrough, press Enter to use the default.</p> 
<h5>Step 4: Select an AWS service</h5> 
<pre><code class="lang-bash">? Select or search for AWS service: s3</code></pre> 
<p>The tool provides autocomplete across <code>@aws-sdk/client-*</code>&nbsp;packages and matches anywhere in the client name. For example, typing ‘s3’ or ‘dynamo’ filters the list to matching packages. It also suggests corrections for typos. For a full list of supported services, see the <a href="https://github.com/aws/aws-sdk-js-v3/tree/main/clients" rel="noopener noreferrer" target="_blank">AWS SDK for JavaScript v3 client packages</a>.</p> 
<h5>Step 5: Wait for operation discovery</h5> 
<pre><code class="lang-bash">Fetching available operations for S3...
  Installing @aws-sdk/client-s3...
  Found 107 operations
  Client: S3Client</code></pre> 
<p>The tool temporarily installs the SDK package in a temporary directory and scans it for available command classes (e.g., ListBucketsCommand, PutObjectCommand).</p> 
<h5>Step 6: Select an operation</h5> 
<pre><code class="lang-bash">? Select or search for operation (kebab-case): list-buckets</code></pre> 
<h5>Step 7: Select a Region</h5> 
<pre><code class="lang-bash">? Select or enter AWS region: us-west-2 - US West (Oregon)</code></pre> 
<p>Regions across commercial, GovCloud, and China partitions are available with autocomplete. GovCloud and China Regions require separate AWS accounts with specific access. For more information, see <a href="https://docs.aws.amazon.com/accounts/latest/reference/manage-acct-regions.html" rel="noopener noreferrer" target="_blank">Managing AWS Regions</a>.</p> 
<h5>Step 8: Review the generated project</h5> 
<p>The tool creates a project directory with the following files:</p> 
<pre><code class="lang-js">// <em>index.js</em>
import { S3Client, ListBucketsCommand } from '@aws-sdk/client-s3';

try {
  const client = new S3Client({ region: 'us-west-2' });
  const input = {}; // Add your input parameters here
  const command = new ListBucketsCommand(input);
  const response = await client.send(command);
  console.log('Success:', response);
} catch (error) {
  console.error('Error:', error);
}</code></pre> 
<pre><code class="lang-json">// <em>package.json</em>
{
  "name": "aws-sdk-repro-a1b2c3d4",
  "version": "1.0.0",
  "type": "module",
  "dependencies": {
    "@aws-sdk/client-s3": "latest"
  },
  "scripts": {
    "start": "node index.js"
  }
}</code></pre> 
<p>The generated code imports the correct client class (<code>S3Client</code>) and command (<code>ListBucketsCommand</code>) directly from the SDK package. It uses the default credentials chain, so it works with <code>aws configure</code> or environment variables. Error handling is included, and the input object is empty and ready for you to add request parameters.</p> 
<h5>Step 9: Run the generated project</h5> 
<pre><code class="lang-bash">cd aws-sdk-repro-a1b2c3d4
npm install
npm start</code></pre> 
<p>For operations like <code>ListBuckets</code>, <code>DescribeInstances</code>, or <code>ListTables</code>, the empty input object works without additional parameters. For operations that require parameters, add them to the input object in <code>index.js</code>. IDE autocomplete will show available fields since the types are already imported.</p> 
<p>The walkthrough above shows a Node.js project. For Browser, the tool generates an <code>index.html</code>, <code>index.js</code> with Cognito credentials, a Vite config, and a <code>COGNITO_SETUP.md</code> guide. For React Native, it scaffolds a full native project with <code>App.js</code>, required polyfills, and Cognito setup. Both include step-by-step instructions for configuring a Cognito identity pools.</p> 
<h2>Clean up</h2> 
<p>The generated projects are standalone directories on your local machine. To clean up:</p> 
<pre><code class="lang-bash">rm -rf aws-sdk-repro-a1b2c3d4</code></pre> 
<p>If you created a Cognito identity pools for Browser or React Native testing, delete the Cognito identity pools and any associated IAM roles that are no longer needed. There are no ongoing AWS costs from the tool itself. Standard API pricing applies only when you run the generated project and make API calls.</p> 
<h2>Conclusion</h2> 
<p>create-aws-sdk-repro automates the setup for creating a minimal SDK project. Pick a service, operation, Region, and environment (Node.js, Browser, or React Native) – the tool handles the rest: correct client imports, credentials configuration, error handling, and a project that runs immediately. It works across Node.js, Browser (with Amazon Cognito), and React Native, covering the most common environments where developers use the AWS SDK for JavaScript v3.</p> 
<p> Whether you’re getting started with a new AWS service, testing SDK behavior in isolation, or troubleshooting an issue, the tool gives you a clean project without the setup overhead. Less time on configuration, more time on the actual work.</p> 
<p>For more on the AWS SDK for JavaScript v3, see our <a href="https://docs.aws.amazon.com/sdk-for-javascript/v3/developer-guide/">Developer Guide</a> and the <a href="https://docs.aws.amazon.com/AWSJavaScriptSDK/v3/latest/">API Reference</a>.</p> 
<p>If you’re working with browser credentials, the <a href="https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-identity.html">Amazon Cognito identity pools documentation</a> covers setup in detail.</p> 
<p>Your feedback is greatly appreciated. You can engage with the AWS SDK for JavaScript team directly by opening a discussion or issue on our <a href="https://github.com/awslabs/create-aws-sdk-repro" rel="noopener noreferrer" target="_blank">GitHub repository</a>.</p> 
<hr style="width: 80%;" /> 
<h2>About the authors</h2>
