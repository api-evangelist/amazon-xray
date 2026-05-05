---
title: "Announcing new output formats in AWS CLI v2"
url: "https://aws.amazon.com/blogs/developer/announcing-new-output-formats-in-aws-cli-v2/"
date: "Sat, 28 Feb 2026 02:22:30 +0000"
author: "Andrew Asseily"
feed_url: "https://aws.amazon.com/blogs/developer/feed/"
---
<p>Amazon Web Services (AWS) is announcing two new features for the <a href="https://aws.amazon.com/cli/" rel="noopener" target="_blank">AWS Command Line Interface (AWS CLI) v2</a>: structured error output and the “off” output format.</p> 
<h2>Structured error output</h2> 
<p>Errors returned from AWS service APIs often include useful details beyond the code and message—bucket names, validation reasons, resource IDs—that were previously hidden unless you used <code>--debug</code>. Now, you can see this error information directly in your error output.</p> 
<p>Starting with AWS CLI v2 version 2.34.0, any additional error details returned from service APIs will now be shown in the stderr output. Additionally, you can configure the AWS CLI to output your errors in alternative structured formats. Control how errors are displayed using the new <code>--cli-error-format</code> <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-error-format.html#cli-error-format-configuring" rel="noopener" target="_blank">CLI flag,</a> the <code>cli_error_format</code> <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-error-format.html#cli-error-format-configuring" rel="noopener" target="_blank">configuration setting</a>, or the <code>AWS_CLI_ERROR_FORMAT</code> <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-error-format.html#cli-error-format-configuring" rel="noopener" target="_blank">environment variable</a>.</p> 
<p>Supported formats for the error format parameter:</p> 
<ul> 
 <li><a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-error-format.html#cli-error-format-enhanced" rel="noopener" target="_blank">enhanced</a> (default) – Error message with additional details displayed inline</li> 
 <li><a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-error-format.html#cli-error-format-json" rel="noopener" target="_blank">json</a> – JSON structure with all error fields</li> 
 <li><a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-error-format.html#cli-error-format-yaml" rel="noopener" target="_blank">yaml</a> – YAML structure with all error fields</li> 
 <li><a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-error-format.html#cli-error-format-text" rel="noopener" target="_blank">text</a> – Tab-delimited error fields</li> 
 <li><a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-error-format.html#cli-error-format-table" rel="noopener" target="_blank">table</a> – ASCII table format</li> 
 <li><a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-error-format.html#cli-error-format-legacy" rel="noopener" target="_blank">legacy</a> – Original error format</li> 
</ul> 
<h3>Accessibility enhancements</h3> 
<p>Since September 2025, AWS CLI errors started including the <code>aws: [ERROR]:</code> prefix for some exceptions. This prefix signals that an error has occurred and supports accessibility best practices and automation use cases. This release ensures the prefix is consistently included for all errors in the enhanced and legacy formats.</p> 
<h3>Example: Using enhanced output error format</h3> 
<div class="hide-language"> 
 <pre><code class="lang-bash">$ aws lambda get-function \
  --function-name nonexistent-function-12345 \
  --cli-error-format enhanced

aws: [ERROR]: An error occurred (ResourceNotFoundException) when calling the GetFunction operation: Function not found: arn:aws:lambda:us-west-2:111122223333:function:nonexistent-function-12345

Additional error details:
Type: User</code></pre> 
</div> 
<h3>Example: Using json output error format</h3> 
<div class="hide-language"> 
 <pre><code class="lang-bash">$ aws lambda get-function \
  --function-name nonexistent-function-12345 \
  --cli-error-format json
{
 "Code": "ResourceNotFoundException",
 "Message": "Function not found: arn:aws:lambda:us-west-2:111122223333:function:nonexistent-function-12345",
 "Type": "User"
}</code></pre> 
</div> 
<h3>Example: Using legacy output error format</h3> 
<div class="hide-language"> 
 <pre><code class="lang-bash">$ aws lambda get-function \
  --function-name nonexistent-function-12345 \
  --cli-error-format legacy

aws: [ERROR]: An error occurred (ResourceNotFoundException) when calling the GetFunction operation: Function not found: arn:aws:lambda:us-west-2:111122223333:function:nonexistent-function-12345</code></pre> 
</div> 
<h2>Turning off CLI output</h2> 
<p>Sometimes, you might want to hide the AWS CLI command output, such as when using a command that may output sensitive information. The <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-output-format.html#off-output" rel="noopener" target="_blank">off format</a> suppresses stdout while still preserving errors on stderr.</p> 
<p>For example, you can <a href="https://docs.aws.amazon.com/secretsmanager/latest/userguide/create_secret.html" rel="noopener" target="_blank">create an AWS Secrets Manager secret</a> without writing the secret ARN or version information to logs:</p> 
<div class="hide-language"> 
 <pre><code class="lang-bash">$ aws secretsmanager create-secret \
    --name my-secret \
    --secret-string "password123" \
    --output off
$ echo $?
0</code></pre> 
</div> 
<p>You can set this using the<code>--output off</code> <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-output-format.html#cli-usage-output-format-how" rel="noopener" target="_blank">CLI flag</a>, setting <code>output = off</code> in your <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-output-format.html#cli-usage-output-format-how" rel="noopener" target="_blank">configuration file</a>, or the <code>AWS_DEFAULT_OUTPUT=off</code> <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-output-format.html#cli-usage-output-format-how" rel="noopener" target="_blank">environment variable</a>.</p> 
<h3>Next Steps</h3> 
<p>To take advantage of these new output features, upgrade your version of the AWS CLI to 2.34.0. For more information, see the <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-usage-error-format.html" rel="noopener" target="_blank">Structured error output</a> and <a href="https://aws.amazon.com/blogs/developer/introducing-agent-plugins-for-aws/" rel="noopener" target="_blank">Output format</a> guides. Please share your questions, comments, and issues with us on <a href="https://github.com/aws/aws-cli/tree/v2" rel="noopener" target="_blank">GitHub</a>.</p>
