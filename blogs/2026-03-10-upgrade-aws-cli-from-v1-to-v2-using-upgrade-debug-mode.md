---
title: "Upgrade AWS CLI from v1 to v2 using upgrade debug mode"
url: "https://aws.amazon.com/blogs/developer/upgrade-aws-cli-from-v1-to-v2-using-upgrade-debug-mode/"
date: "Tue, 10 Mar 2026 15:00:04 +0000"
author: "Ahmed Moustafa"
feed_url: "https://aws.amazon.com/blogs/developer/feed/"
---
<p>Upgrading from <a href="https://docs.aws.amazon.com/cli/v1/userguide/cli-chap-welcome.html" rel="noopener" target="_blank">AWS Command Line Interface (AWS CLI) v1</a> to <a href="https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html" rel="noopener" target="_blank">AWS CLI v2</a> can be challenging and time-consuming due to changes introduced in AWS CLI v2 that can potentially break your existing workflows. If you don’t properly address breaking changes in your scripts or workflows, then executing these workflows after upgrading to AWS CLI v2 may result in unintended consequences, such as failing commands or misconfiguring resources in your AWS account.</p> 
<p>AWS CLI v1’s upgrade debug mode helps you identify and resolve these issues before upgrading, for a safer and seamless transition. This mode detects usage of features in AWS CLI v1 that have been updated with breaking changes in AWS CLI v2, and outputs a warning for each detection.</p> 
<p>In this post, we’ll walk you through using AWS CLI v1’s upgrade debug mode to identify potential breaking changes, resolve compatibility issues, and safely transition your workflows to v2.</p> 
<h2>Getting Started</h2> 
<p>You’ll start by verifying you have the correct version of AWS CLI v1 to use upgrade debug mode, then you’ll use this mode to test commands in AWS CLI v1 for usage of features that were updated with breaking changes in AWS CLI v2. Then, you’ll review the <a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html" rel="noopener" target="_blank">AWS CLI v2 breaking changes list</a> in the <a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration.html" rel="noopener" target="_blank">Migration guide for the AWS CLI version 2</a> to manually verify whether your workflows may be broken by upgrading. Finally, you’ll follow guidance to mitigate breaking your workflows and safely upgrade to AWS CLI v2.</p> 
<h3>AWS CLI v1</h3> 
<p>The following steps walk you through using upgrade debug mode to identify potential breaking changes in your existing AWS CLI v1 usage, resolve compatibility issues, and safely transition to AWS CLI v2.</p> 
<h4>Step 1: Verify you are using AWS CLI v1 version 1.44.0 or higher.</h4> 
<p>We released the upgrade debug mode feature to the AWS CLI in version 1.44.0.</p> 
<p>Using AWS CLI v1, run <code>aws --version</code>, and verify that the AWS CLI version is 1.44.0 or higher.</p> 
<p>If the version is older than 1.44.0, see our <a href="https://docs.aws.amazon.com/cli/v1/userguide/cli-chap-install.html" rel="noopener" target="_blank">Developer Guide</a> for instructions to update to a later version.</p> 
<h4>Step 2: Test your AWS CLI v1 usage with AWS CLI upgrade debug mode</h4> 
<p>Set the <code>AWS_CLI_UPGRADE_DEBUG_MODE</code> environment variable to <code>true</code> to detect usage of features broken in AWS CLI v2. Alternatively, you can enable this functionality at the command-level using the <code>--v2-debug</code> command line option. If you are upgrading the AWS CLI in existing scripts or workflows to use v2, we recommend testing each AWS CLI command used with this functionality enabled before upgrading them to use AWS CLI v2.</p> 
<p>We recommend performing this step in the same environment that you will upgrade to use AWS CLI v2, since the execution environment determines whether commands will experience breaking changes.</p> 
<p>For example, suppose you have a script that executes the AWS CLI command below:</p> 
<pre><code>aws secretsmanager update-secret --secret-id SECRET-NAME \
  --secret-binary file://BINARY-SECRET.json
</code></pre> 
<p>Execute the command with the <code>AWS_CLI_UPGRADE_DEBUG_MODE</code> set to true—or with the <code>--v2-debug</code> flag—and check the output for the text “AWS CLI v2 UPGRADE WARNING”. Example output with the environment variable configured is shown below:</p> 
<pre><code>$ aws secretsmanager update-secret --secret-id SECRET-NAME \
  --secret-binary file://BINARY-SECRET.json

AWS CLI v2 UPGRADE WARNING: When specifying a blob-type parameter, AWS CLI v2 will 
assume the parameter value is base64-encoded. This is different from v1 behavior, 
where the AWS CLI will automatically encode the value to base64. To retain v1 
behavior in AWS CLI v2, set the `cli_binary_format` configuration variable to 
`raw-in-base64-out`. See 
<a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html#cliv2-migration-binaryparam." rel="noopener noreferrer">https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html#cliv2-migration-binaryparam.</a>

{
    "ARN": "ARN",
    "Name": "SECRET-NAME",
    "VersionId": "VERSION-ID"
}
</code></pre> 
<h4>Step 3: Use the warnings to prepare for AWS CLI v2</h4> 
<p>If breaking changes were detected in step 2, the warnings provide guidance for preparing for the AWS CLI v2 upgrade. Some breaking changes can be mitigated prior to upgrading to AWS CLI v2 by modifying the command or execution environment; the warnings identified in step 2 include links to our <a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html" rel="noopener" target="_blank">AWS CLI v2 breaking changes list</a> that details options to mitigate the breakage.</p> 
<p>In the previous example, the warning explains that AWS CLI v2 will assume that the contents of <code>BINARY-SECRET.json</code> will be encoded in base64.</p> 
<p>Following the instructions in the warning, you’ll configure the <code>cli_binary_format</code> variable to <code>raw-in-base64-out</code> in the <a href="https://docs.aws.amazon.com/cli/v1/userguide/cli-configure-files.html" rel="noopener" target="_blank">configuration file</a>. Even though <code>cli_binary_format</code> is not a valid configuration setting in AWS CLI v1, it prepares your environment for AWS CLI v2 by configuring AWS CLI v2 to retain the same behavior as AWS CLI v1.</p> 
<p>You’ll configure <code>cli_binary_format</code> according to the instructions using the following command:</p> 
<pre><code>aws configure set cli_binary_format raw-in-base64-out
</code></pre> 
<h4>Step 4: Verify resolution of warnings</h4> 
<p>For breaking changes mitigated in step 3, you’ll re-run the command to verify the warning is no longer printed.</p> 
<p>Proceeding with the example, you configured the <code>cli_binary_format</code> variable to <code>raw-in-base64-out</code> in step 3. You’ll now re-run the command to verify the mitigation warning is resolved:</p> 
<pre><code>aws secretsmanager update-secret --secret-id SECRET-NAME \
    --secret-binary file://BINARY-SECRET.json 
{
    "ARN": "ARN",
    "Name": "SECRET-NAME",
    "VersionId": "VERSION-ID"
}
</code></pre> 
<p>The warning is no longer printed, signaling that this command is now compatible with AWS CLI v2.</p> 
<p>If you used the <code>--v2-debug</code> argument instead of the <code>AWS_CLI_UPGRADE_DEBUG_MODE</code> environment variable in step 2, remember to remove the flag from the command before upgrading to version 2.</p> 
<h4>Step 5: Manually review for breaking changes</h4> 
<p>After using upgrade debug mode to automatically detect usage of features that were updated with breaking changes, you will now manually review your AWS CLI usage by reviewing our <a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html" rel="noopener" target="_blank">breaking changes list</a> and <a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration.html" rel="noopener" target="_blank">AWS CLI v2 Migration Guide</a>.</p> 
<h4>Step 6: Upgrade to AWS CLI v2</h4> 
<p>After preparing for the breaking changes identified in the previous steps, you will now upgrade to AWS CLI v2 following the <a href="https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html" rel="noopener" target="_blank">installation guide</a>.</p> 
<h2>Limitations</h2> 
<p>The upgrade debug mode feature does not currently support every breaking change introduced with AWS CLI v2, and has false positive cases where it issues a warning even if no breaking changes are actually present.</p> 
<p>Additionally, some of the detection depends on API responses, as well as the execution environment running the AWS CLI. For this reason, we recommend running this feature against an AWS account and execution environment that reflect your production workflows as close as possible.</p> 
<p>For more details on the limitations of upgrade debug mode, see <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-upgrade-debug-mode.html" rel="noopener" target="_blank">Using upgrade debug mode to upgrade AWS CLI version 1 to AWS CLI version 2</a> in <a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration.html" rel="noopener" target="_blank">Migration guide for the AWS CLI version 2</a>.</p> 
<p>We strongly recommend customers understand our <a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html" rel="noopener" target="_blank">breaking changes list</a> published in our <a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration.html" rel="noopener" target="_blank">AWS CLI v2 Migration Guide</a>.</p> 
<p>The only breaking change not supported by the upgrade debug mode is that <a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration-changes.html#cliv2-migration-return-codes" rel="noopener" target="_blank">AWS CLI version 2 provides more consistent return codes across commands</a>.</p> 
<h2>Conclusion</h2> 
<p>In this blog post, we showed you how to get started with the new upgrade debug mode. If you’re interested in using this feature to assist your upgrade from AWS CLI v1 to AWS CLI v2, try out upgrade debug mode. To learn more, visit <a href="https://docs.aws.amazon.com/cli/latest/userguide/cli-upgrade-debug-mode.html" rel="noopener" target="_blank">Using upgrade debug mode to upgrade AWS CLI version 1 to AWS CLI version 2</a> in our <a href="https://docs.aws.amazon.com/cli/latest/userguide/cliv2-migration.html" rel="noopener" target="_blank">AWS CLI v2 Migration Guide</a>. We would love your feedback! You can reach out to us by creating a <a href="https://github.com/aws/aws-cli/issues/new/choose" rel="noopener" target="_blank">GitHub Issue</a>.</p>
