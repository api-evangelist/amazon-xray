---
title: "AWS SDK for .NET V3 Maintenance Mode Announcement"
url: "https://aws.amazon.com/blogs/developer/aws-sdk-for-net-v3-maintenance-mode-announcement/"
date: "Wed, 04 Mar 2026 19:35:48 +0000"
author: "Muhammad Othman"
feed_url: "https://aws.amazon.com/blogs/developer/feed/"
---
<p>In alignment with our <a href="https://aws.amazon.com/blogs/developer/general-availability-of-aws-sdk-for-net-v4-0/" rel="noopener noreferrer" target="_blank">V4.0 GA announcement</a> and <a href="https://docs.aws.amazon.com/sdkref/latest/guide/maint-policy.html" rel="noopener noreferrer" target="_blank">SDKs and Tools Maintenance Policy</a>, version 3 of the <a href="https://aws.amazon.com/sdk-for-net/" rel="noopener noreferrer" target="_blank">AWS SDK for .NET</a> will enter maintenance mode on March 1, 2026, and reach end-of-support on June 1, 2026. Starting March 1, 2026 we will stop adding regular updates to V3 and will only provide security updates until end-of-support begins.</p> 
<h2>Support Timeline</h2> 
<p>When we announced the general availability of AWS SDK for .NET V4 on April 28, 2025, we committed to a support timeline tied to the <a href="https://aws.amazon.com/powershell/" rel="noopener noreferrer" target="_blank">AWS Tools for PowerShell</a>, which depends on the SDK. With AWS Tools for PowerShell V5 reaching <a href="https://aws.amazon.com/blogs/developer/aws-tools-for-powershell-v5-now-generally-available/" rel="noopener noreferrer" target="_blank">general availability in August 2025</a>, the 6-month support window for V3 began. For more details on the original support commitment, see the&nbsp;<a href="https://aws.amazon.com/blogs/developer/general-availability-of-aws-sdk-for-net-v4-0/" rel="noopener noreferrer" target="_blank">V4.0 GA announcement</a>.</p> 
<p>The following table outlines the level of support for each phase of the SDK lifecycle.</p> 
<table border="1px" cellpadding="10px" class="styled-table"> 
 <tbody> 
  <tr> 
   <td style="padding: 10px; border: 1px solid #dddddd;"><strong>SDK Lifecycle Phase</strong></td> 
   <td style="padding: 10px; border: 1px solid #dddddd;"><strong>Start Date</strong></td> 
   <td style="padding: 10px; border: 1px solid #dddddd;"><strong>End Date</strong></td> 
   <td style="padding: 10px; border: 1px solid #dddddd;"><strong>Support Level</strong></td> 
  </tr> 
  <tr> 
   <td style="padding: 10px; border: 1px solid #dddddd;">General Availability</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">July&nbsp;28,&nbsp;2015</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">February 28, 2026</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">During this phase, the SDK is fully supported. AWS will provide regular SDK releases that include support for new services, API updates for existing services, as well as bug and security fixes.</td> 
  </tr> 
  <tr> 
   <td style="padding: 10px; border: 1px solid #dddddd;">Maintenance Mode</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">March 1, 2026</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">May 31, 2026</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">During the maintenance mode, AWS will limit SDK releases to address critical bug fixes and security issues only. AWS SDK for .NET v3.x will not receive API updates for new or existing services or be updated to support new regions.</td> 
  </tr> 
  <tr> 
   <td style="padding: 10px; border: 1px solid #dddddd;">End-of-Support</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">June 1, 2026</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">N/A</td> 
   <td style="padding: 10px; border: 1px solid #dddddd;">AWS SDK for .NET v3.x will no longer receive updates or releases. Previously published releases will continue to be available via public package managers and the code will remain on GitHub.</td> 
  </tr> 
 </tbody> 
</table> 
<h2>Next Steps</h2> 
<p>We encourage the AWS SDK for .NET community to begin planning your migration to V4 as soon as possible:</p> 
<ul> 
 <li>Review the <a href="https://docs.aws.amazon.com/sdk-for-net/v4/developer-guide/net-dg-v4.html" rel="noopener noreferrer" target="_blank">Migration Guide</a> to understand the breaking changes.</li> 
 <li>Test your applications with V4 in a development environment.</li> 
 <li>Update your code to accommodate the changes.</li> 
 <li>Provide feedback through our <a href="https://github.com/aws/aws-sdk-net" rel="noopener noreferrer" target="_blank">GitHub repository</a>.</li> 
</ul> 
<h2>Conclusion</h2> 
<p>With the maintenance mode transition now in effect and end of support on June 1st, 2026, we recommend prioritizing your migration planning to ensure a smooth transition. <a href="https://docs.aws.amazon.com/sdk-for-net/v4/developer-guide/net-dg-v4.html" rel="noopener noreferrer" target="_blank">Migration documentation</a> is available to guide you through the update process.</p> 
<p>For questions or issues that arise while updating to the V4 SDK, please use the GitHub repository’s <a href="https://github.com/aws/aws-sdk-net/discussions" rel="noopener noreferrer" target="_blank">discussion forums</a> or open GitHub <a href="https://github.com/aws/aws-sdk-net/issues" rel="noopener noreferrer" target="_blank">issues </a>to reach out to us. If you find dependencies that are preventing you from updating to V4, please let us know to see if we can help.</p>
