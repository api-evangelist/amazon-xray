---
title: "Upgrading AWS CLI From v1 to v2 Using the Migration Tool"
url: "https://aws.amazon.com/blogs/developer/upgrading-aws-cli-from-v1-to-v2-using-the-migration-tool/"
date: "Fri, 27 Mar 2026 22:53:53 +0000"
author: "Ahmed Moustafa"
feed_url: "https://aws.amazon.com/blogs/developer/feed/"
---
<p>Upgrading from <a href="https://docs.aws.amazon.com/cli/v1/userguide/cli-chap-welcome.html" rel="noopener" target="_blank">AWS Command Line Interface (AWS CLI) v1 </a>to <a href="https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html" rel="noopener" target="_blank">AWS CLI v2</a> brings valuable improvements, but requires attention to several changes that may affect your existing workflows, such as failing commands, or misconfiguration.</p> 
<p>The AWS CLI v1-to-v2 Migration Tool helps you identify and resolve issues before upgrading, making transition easier. It analyzes bash scripts containing AWS CLI v1 commands where behavior differs in AWS CLI v2. The tool will either suggest a change to a command or guide you to resolve a potential risk. It can also automatically create an updated version of the script with implemented changes. Where applicable, the migration tool will change the commands in a way that preserves AWS CLI version 1 behavior.</p> 
<p>The AWS CLI v1-to-v2 Migration Tool is a standalone tool compatible with <i>any</i>&nbsp;version of AWS CLI v1, and does not require executing AWS CLI commands.&nbsp;Compared to Upgrade Debug Mode, an alternative solution built into AWS CLI version <code>1.44.0</code> or later, the Migration Tool offers broader compatibility and works independently of your CLI installation. For a thorough comparison between the Upgrade Debug Mode and the AWS CLI v1-to-v2 Migration Tool see <a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration.html#cliv2-migration-choosing-migration-tool" rel="noopener" target="_blank">Choosing Between Upgrade Debug Mode and AWS CLI v1-to-v2 Migration Tool</a><b> </b>in our <a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration.html" rel="noopener" target="_blank">Migration guide for the AWS CLI version 2</a>.</p> 
<p>In this post, we’ll walk you through using&nbsp;AWS CLI v1-to-v2 Migration Tool to identify potential breaking changes, resolve compatibility issues, and safely transition your scripts to v2.</p> 
<h2>Prerequisites</h2> 
<p>Before you begin, you’ll need Python version 3.9 or later, and pip installed on your machine. See the <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-migration-tool.html#migration-tool-prerequisites" rel="noopener" target="_blank">Prerequisites</a> in <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-migration-tool.html" rel="noopener" target="_blank">Using AWS CLI v1-to-v2 Migration Tool to upgrade AWS CLI version 1 to AWS CLI version 2</a>&nbsp;for instructions to install these prerequisites.</p> 
<h2>Getting Started</h2> 
<p>You’ll start by installing the AWS CLI v1-to-v2 Migration Tool. Then, you’ll use this tool to analyze bash scripts for AWS CLI v1 commands that may need to be updated before upgrading to AWS CLI v2.&nbsp;Then, you’ll review the&nbsp;<a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html" rel="noopener" target="_blank">AWS CLI v2 breaking changes list</a>&nbsp;in the&nbsp;<a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration.html" rel="noopener" target="_blank">Migration guide for the AWS CLI version 2</a>&nbsp;to manually verify whether your workflows may be broken by upgrading, and safely upgrade to AWS CLI v2.</p> 
<h3>Step 1: Install the&nbsp;AWS CLI v1-to-v2 Migration Tool</h3> 
<p>See <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-migration-tool.html#migration-tool-installation" rel="noopener" target="_blank">Installation</a> in <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-migration-tool.html" rel="noopener" target="_blank">Using AWS CLI v1-to-v2 Migration Tool to upgrade AWS CLI version 1 to AWS CLI version 2</a> for instructions to install the AWS CLI v1-to-v2 Migration Tool.</p> 
<h3>Step 2: Lint a bash script using interactive mode</h3> 
<p>Next, you’ll run the migration tool in interactive mode. Interactive mode walks you through each flagged command one at a time. For each detection, it will suggest a change to make the command have the same behavior in AWS CLI v2.</p> 
<p>For this blog post, we’ll use&nbsp;the following example bash script, which uses AWS CLI v1 to upload an AWS CloudFormation template to Amazon Simple Storage Service (Amazon S3), copy the template to a backup Amazon S3 bucket, and create a CloudFormation stack from the template.</p> 
<div class="hide-language"> 
 <pre><code class="lang-bash">#!/bin/bash
set -e

TEMPLATE="$1"
BUCKET="$2"
BACKUP="$3"
STACK_NAME="$4"

if [ -z "$TEMPLATE" ] || [ -z "$BUCKET" ] || [ -z "$BACKUP" ] || [ -z "$STACK_NAME" ]; then
&nbsp;&nbsp; &nbsp;echo "Usage: $0&nbsp;&lt;template-file&gt; &lt;bucket&gt; &lt;backup-bucket&gt; &lt;stack-name&gt;"
&nbsp;&nbsp; &nbsp;exit 1
fi

TMPKEY="cloudformation/$(basename "$TEMPLATE")"
TIMESTAMP=$(date +%Y%m%d-%H%M%S)
BACKUP_KEY="cloudformation/$TIMESTAMP-$(basename "$TEMPLATE")"

# Upload template
aws s3 cp $TEMPLATE s3://$BUCKET/$TMPKEY

# Copy template to backup bucket
aws s3 cp s3://$BUCKET/$TMPKEY&nbsp;s3://$BACKUP/$BACKUP_KEY

# Create a stack from the template
aws cloudformation create-stack \
&nbsp;&nbsp;--stack-name "$STACK_NAME"&nbsp;\
&nbsp;&nbsp;--template-body "https://s3.amazonaws.com/$BUCKET/$TMPKEY"

echo "Stack creation initiated. Stack ID: $(
&nbsp;&nbsp;aws cloudformation describe-stacks \
&nbsp;&nbsp; &nbsp;--stack-name "$STACK_NAME" \
&nbsp;&nbsp; &nbsp;--query 'Stacks[0].StackId' \
&nbsp;&nbsp; &nbsp;--output text \
&nbsp; &nbsp; --cli-input-json file://describe_stacks_input.json
)"</code></pre> 
</div> 
<p>You will use the command below to use the migration tool to analyze the bash script <code>upload_s3_files.sh</code>, suggest fixes, and write the modified script to the path <code>upload_s3_files_v2.sh</code> in interactive mode. For the sake of demonstration, this blog post does not include every finding that gets detected in the example script:</p> 
<div class="hide-language"> 
 <pre><code class="lang-bash">$ migrate-aws-cli --script upload_s3_files.sh&nbsp;--output upload_s3_files_v2.sh \
&nbsp;&nbsp;--interactive
&nbsp;&nbsp;
19 19│ aws s3 cp $TEMPLATE s3://$BUCKET/$TMPKEY
20 20│ 
21 21│ # Copy template to backup bucket
22 &nbsp; │-aws s3 cp s3://$BUCKET/$TMPKEY s3://$BACKUP/$BACKUP_KEY
&nbsp;&nbsp; 22│+aws s3 cp s3://$BUCKET/$TMPKEY s3://$BACKUP/$BACKUP_KEY --copy-props none
23 23│ 
24 24│ # Create a stack from the template
25 25│ aws cloudformation create-stack \

script.sh:22 [s3-copy] In AWS CLI v2, object properties will be copied from the 
source in multipart copies between S3 buckets. If a copy is or becomes multipart 
after upgrading to AWS CLI v2, extra API calls will be made. See 
<a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html#cliv2-migration-s3-copy-metadata." rel="noopener noreferrer">https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html#cliv2-migration-s3-copy-metadata.</a>

Apply this fix? [y] yes, [n] no, [a] accept all of type, [r] reject all of type, 
[u] update all, [s] save and exit, [q] quit:</code></pre> 
</div> 
<p>In the preceding finding, the associated breaking change is <a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html#cliv2-migration-s3-copy-metadata" rel="noopener" target="_blank">Improved Amazon S3 handling of file properties and tags for multipart copies</a>. The suggested fix, given in a form similar to a Git diff, is to add the <code>--copy-props none</code>&nbsp;flag to the command. Adding the suggested flag will preserve AWS CLI v1 behavior in AWS CLI v2.</p> 
<p>The following output snippet shows another finding:</p> 
<div class="hide-language"> 
 <pre><code class="lang-bash">16 16│ BACKUP_KEY="cloudformation/$TIMESTAMP-$(basename "$TEMPLATE")"
17 17│ 
18 18│ # Upload template
19 &nbsp; │-aws s3 cp $TEMPLATE s3://$BUCKET/$TMPKEY
&nbsp;&nbsp; 19│+aws s3 cp $TEMPLATE s3://$BUCKET/$TMPKEY&nbsp;--cli-binary-format raw-in-base64-out
20 20│ 
21 21│ # Copy template to backup bucket
22 22│ aws s3 cp "s3://$BUCKET/$TMPKEY" "s3://$BACKUP/$BACKUP_KEY"

examples/upload_s3_files.sh:19 [binary-params-base64] In AWS CLI v2, an input 
parameter typed as binary large object (BLOB) expects the input to be base64-encoded. 
If using a BLOB-type input parameter, retain v1 behavior after upgrading to AWS CLI 
v2&nbsp;by adding `--cli-binary-format raw-in-base64-out`. See 
<a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html#cliv2-migration-binaryparam." rel="noopener noreferrer">https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html#cliv2-migration-binaryparam.</a>

Apply this fix? [y] yes, [n] no, [a] accept all of type, [r] reject all of type, 
[u] update all, [s] save and exit, [q] quit:</code></pre> 
</div> 
<p>In the preceding detection, the associated breaking change is that&nbsp;<a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html#cliv2-migration-binaryparam" rel="noopener" target="_blank">Binary parameters are passed as base64-encoded strings by default</a>. The suggested fix, is to add the <code>--cli-binary-format raw-in-base64-out</code>&nbsp;flag to the command. Adding the suggested flag will preserve AWS CLI v1 behavior in AWS CLI v2.</p> 
<p>Note that in this particular case, we are not using a binary-type parameter in the <code>aws s3 cp</code>&nbsp;command.&nbsp;This highlights a core behavior of the migration tool: by design, it errs on the side of caution when detecting potential issues, flagging changes that might be breaking even when uncertain, provided the suggested fix won’t alter the code’s behavior.</p> 
<p>The following output snippet shows another finding:</p> 
<div class="hide-language"> 
 <pre><code class="lang-bash">27 27│ &nbsp;--template-body "https://s3.amazonaws.com/$BUCKET/$TEMPLATE_KEY" --cli-binary-format raw-in-base64-out --no-cli-pager
28 28│
29 29│echo "Stack creation initiated. Stack ID: $(
30 30│ &nbsp;aws cloudformation describe-stacks \
31 31│ &nbsp; &nbsp;--stack-name "$STACK_NAME" \
32 32│ &nbsp; &nbsp;--query 'Stacks[0].StackId' \
33 33│ &nbsp; &nbsp;--output text \
34 34│ &nbsp; &nbsp;--cli-input-json file://describe_stacks_input.json --cli-binary-format raw-in-base64-out --no-cli-pager
35 35│)"

examples/upload_s3_files.sh:30 [MANUAL REVIEW REQUIRED] [cli-input-json] In AWS CLI 
v2, specifying pagination parameters via `--cli-input-json` turns off automatic 
pagination. If pagination-related parameters are present in the input JSON specified 
with `--cli-input-json`, remove the pagination parameters from the input JSON to 
retain v1 behavior. See 
<a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html#cliv2-migration-skeleton-paging." rel="noopener noreferrer">https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html#cliv2-migration-skeleton-paging.</a>

[n] next, [s] save, [q] quit:</code></pre> 
</div> 
<p>In the preceding detection, the detected breaking change is&nbsp;<a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html#cliv2-migration-skeleton-paging" rel="noopener" target="_blank">AWS CLI version 2 is more consistent with paging parameters</a>.&nbsp;The migration tool cannot automatically modify the script in this case, so the detection is flagged with&nbsp;<code>[MANUAL REVIEW REQUIRED]</code>.</p> 
<p>For detections that require manual fixes, such as the example, you’ll enter <code>n</code> and manually address the finding after the migration tool finishes executing.</p> 
<p>After all detections are displayed, a summary is printed, including the number of issues found and the path to the modified script:</p> 
<div class="hide-language"> 
 <pre><code class="lang-bash">Found 10 issue(s). 9 fixed. 1 require(s) manual review.
Changes written to: upload_s3_files_v2.sh</code></pre> 
</div> 
<p>To resolve the detections that were flagged for manual review, follow the guidance in the suggested actions.</p> 
<h3>Step 3: Upgrade to AWS CLI v2</h3> 
<p>Customers are responsible for safely migrating their scripts; using the migration tool does not guarantee that all commands will have the same behavior in AWS CLI v2.&nbsp;To complete a manual review, reference the&nbsp;<a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html" rel="noopener" target="_blank">breaking changes list</a>&nbsp;in the&nbsp;<a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration.html" rel="noopener" target="_blank">AWS CLI v2 Migration Guide</a>.</p> 
<p>After going through and applying any required changes identified in the previous steps, you are now ready to upgrade to AWS CLI v2 following the <a href="https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html" rel="noopener" target="_blank">installation guide</a>.</p> 
<h3>Step 4: Uninstall migration tool if no longer needed</h3> 
<p>After migration, you can uninstall the migration tool and remove original scripts if no longer needed.</p> 
<h2>Important Considerations</h2> 
<p>The AWS CLI v1-to-v2 Migration Tool uses static analysis to identify most compatibility considerations in your scripts. However, some scenarios—such as parameters stored in variables or determined at runtime—fall outside the tool’s detection scope and require manual review.</p> 
<p>For more details on the limitations of the AWS CLI v1-to-v2 Migration Tool, see&nbsp;<a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-migration-tool.html#migration-tool-limitations" rel="noopener" target="_blank">Limitations</a> in <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-migration-tool.html" rel="noopener" target="_blank">Using AWS CLI v1-to-v2 Migration Tool to upgrade AWS CLI version 1 to AWS CLI version 2</a>.</p> 
<p>We strongly recommend customers understand our <a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html" rel="noopener" target="_blank">breaking changes list</a> published in our <a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration.html" rel="noopener" target="_blank">AWS CLI v2 Migration Guide</a>.</p> 
<h2>Conclusion</h2> 
<p>In this blog post, we showed you how to get started with the new AWS CLI v1-to-v2 Migration Tool to assist your upgrade from AWS CLI v1 to AWS CLI v2. To learn more, visit <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-migration-tool.html" rel="noopener" target="_blank">Using AWS CLI v1-to-v2 Migration Tool to upgrade AWS CLI version 1 to AWS CLI version 2</a>. We would love your feedback!&nbsp;You can also open a discussion or issue on <a href="https://github.com/aws/aws-cli/issues/new?template=migration-tool.yml" rel="noopener" target="_blank">GitHub</a>. Thank you for using the AWS CLI!</p> 
<p>Have you encountered challenges migrating from AWS CLI v1 to AWS CLI v2? Share your experience in the comments below.</p>
