---
title: "AWS Tools for PowerShell v4 Maintenance Mode Announcement"
url: "https://aws.amazon.com/blogs/developer/aws-tools-for-powershell-v4-maintenance-mode-announcement/"
date: "Fri, 27 Feb 2026 18:25:37 +0000"
author: "Sanket Tangade"
feed_url: "https://aws.amazon.com/blogs/developer/feed/"
---
<p>In alignment with our previous <a href="https://aws.amazon.com/blogs/devops/announcing-the-end-of-support-for-aws-tools-for-powershell-v4/" rel="noopener noreferrer" target="_blank">announcement in August 2025</a> and <a href="https://docs.aws.amazon.com/sdkref/latest/guide/maint-policy.html" rel="noopener noreferrer" target="_blank">SDKs and Tools Maintenance Policy</a>, version 4 of the <a href="https://aws.amazon.com/powershell/" rel="noopener noreferrer" target="_blank">AWS Tools for PowerShell</a> (AWS Tools for PowerShell v4.x) will enter maintenance mode on March 1, 2026 and reach end-of-support on June 1, 2026.</p> 
<p>Beginning March 1, 2026, AWS Tools for PowerShell v4.x will enter maintenance mode and will only receive critical bug fixes and security updates. We will not update it to support new AWS services, new service features, or changes to existing services. Existing applications that use AWS Tools for PowerShell v4.x will continue to function as intended unless there is a fundamental change to how an AWS service works. This is uncommon, and we will announce it broadly if it happens. After June 1, 2026, when AWS Tools for PowerShell v4.x reaches end-of-support, it will no longer receive any updates or releases.</p> 
<h2>End of Support Timeline for Version 4</h2> 
<p>The following table outlines the level of support for each phase of the SDK lifecycle.</p> 
<table border="1px" cellpadding="6px" class="styled-table"> 
 <tbody> 
  <tr> 
   <td style="padding: 10px; border: 1px solid #dddddd;"><strong>SDK Lifecycle Phase</strong></td> 
   <td style="padding: 10px; border: 1px solid #dddddd;"><strong>Start Date</strong></td> 
   <td style="padding: 10px; border: 1px solid #dddddd;"><strong>End Date</strong></td> 
   <td style="padding: 10px; border: 1px solid #dddddd;"><strong>Support Level</strong></td> 
  </tr> 
  <tr> 
   <td style="padding: 10px; border: 1px solid #dddddd;">General Availability</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">July 28, 2015</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">February 28, 2026</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">During this phase, the SDK is fully supported. AWS will provide regular SDK releases that include support for new services, API updates for existing services, as well as bug and security fixes.</td> 
  </tr> 
  <tr> 
   <td style="padding: 10px; border: 1px solid #dddddd;">Maintenance Mode</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">March 1, 2026</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">May 31, 2026</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">During the maintenance mode, AWS will limit releases to address critical bug fixes and security issues only. AWS Tools for PowerShell v4.x will not receive API updates for new or existing services or be updated to support new regions.</td> 
  </tr> 
  <tr> 
   <td style="padding: 10px; border: 1px solid #dddddd;">End-of-Support</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">June 1, 2026</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">N/A</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">AWS Tools for PowerShell v4.x will no longer receive updates or releases. Previously published releases will continue to be available via public package managers and the code will remain on GitHub.</td> 
  </tr> 
 </tbody> 
</table> 
<h2>Conclusion</h2> 
<p>We recommend upgrading to the latest major version of AWS Tools for PowerShell v5.x by using the <a href="https://docs.aws.amazon.com/powershell/v5/userguide/migrating-v5.html" rel="noopener noreferrer" target="_blank">migration guide</a>. This major version includes, but is not limited to, performance enhancements, bug fixes, modern .NET libraries and frameworks, and the latest AWS service updates. Upgrading enables you to leverage the latest services and innovations from AWS.</p> 
<p>To learn more, refer to the following resources:</p> 
<ul> 
 <li>The AWS Tools for PowerShell<a href="https://aws.amazon.com/powershell/" rel="noopener noreferrer" target="_blank"> landing page</a> contains links to the getting started guide, key features, examples, and links to additional resources.</li> 
 <li>The <a href="https://docs.aws.amazon.com/powershell/v5/userguide/migrating-v5.html" rel="noopener noreferrer" target="_blank">Migrating to version 5 of the AWS Tools for PowerShell guide</a> provides instructions for migrating and explains the changes between the two versions.</li> 
 <li>The <a href="https://aws.amazon.com/blogs/developer/aws-tools-for-powershell-v5-now-generally-available/" rel="noopener noreferrer" target="_blank">AWS Tools for PowerShell v5.x GA blog post</a> outlines the motivation for launching AWS Tools for PowerShell v5.x and includes the benefits over AWS Tools for PowerShell v4.x.</li> 
 <li><a href="https://docs.aws.amazon.com/powershell/v5/userguide/powershell_code_examples.html" rel="noopener noreferrer" target="_blank">AWS Tools for PowerShell Code Examples</a> provide code examples to help you use v5.x.</li> 
</ul> 
<h2>Feedback</h2> 
<p>If you need assistance or have feedback, reach out to your usual AWS support contacts. You can also open a <a href="https://github.com/aws/aws-tools-for-powershell/discussions" rel="noopener noreferrer" target="_blank">discussion</a> or <a href="https://github.com/aws/aws-tools-for-powershell/issues" rel="noopener noreferrer" target="_blank">issue</a> on GitHub. Thank you for using AWS Tools for PowerShell.</p> 
<hr />
