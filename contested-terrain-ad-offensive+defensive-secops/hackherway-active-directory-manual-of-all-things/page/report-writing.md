# Report Writing

Report Writing

Introduction

Report writing is an essential component of any security engagement, whether it is a pentest report, a red teaming report, or a submission for a bug bounty program. The way information is structured, organized, and presented significantly influences the reception of your report. In this chapter, we will dive into how a penetration testing report should be crafted, structured, and conveyed to effectively communicate findings.

Reporting Audience

The first step to writing a pentest report is understanding the audience that the report is going to be addressed to. While this may vary based on an organization’s structure, a pentest report usually caters to three distinct audience categories:

_**Executives:**_ This group comprises the CEO, board members, and senior leadership. Typically, they might read only the initial pages of the report such as the executive summary and strategic recommendations; therefore, it is imperative to immediately highlight critical metrics, potential financial losses, and regulatory fines in this section.

_**Security/Technology Executives:**_ This segment consists of executives overseeing technology and security portfolios, such as CISO, CIO, and CTO. They are interested in a more detailed overview than the top executives are, focusing on sections like the summary of findings, overall strengths and weaknesses, risk assessment report, and strategic recommendations.

_**Technical Teams:**_ This audience includes security teams, development squads, and operations units. They are keen on diving dep into the technical aspects of the report. This group will scrutinize your technical findings, try to replicate the vulnerabilities, and consider your technical recommendations.

Executive Summary

The executive summary is one of the first sections of every pentesting report, highlighting the key outcomes of the engagement. The executive summary should be concise, ideally no longer than a single page. It is essential to highlight the key findings and outcomes of the report in a business-centric language, ensuring that the report’s primary insights are easily accessible to non-technical stakeholders. Top executives, for instance, are typically more concerned with the broader security implications for the organization rather than the specific tools used to identify vulnerabilities on the company’s public-facing portal.

Structure of an Executive Summary

Let’s talk about the structure of an executive summary:

_**Introduction:**_ The opening lines should detail the type of engagement undertaken, the relevant dates, and primary objective of the pentest.

_**Engagement Highlights:**_ This section provides a concise overview of the entire pentest, articulated in a business-centric language. It addresses the critical aspects such as the presence of any crucial vulnerabilities, their business impact, and whether it was possible to access the sensitive data and the overall security posture of the company.

_**Key Findings:**_ The _“Key Findings”_ section in a report primarily highlights the most crucial and actionable insights from the broader analysis. It should cover vulnerabilities, risks, or gaps identified during the evaluation, providing decision-makers with a clear understanding of the current state, potential implications, and areas requiring immediate attention.

_**Business Implications:**_ This segment covers potential repercussions if findings are not addresses, such as financial loss, reputational loss, and/or possible regulatory fines.

_**Strategic Recommendations:**_ In this section, all technical findings are grouped into their main classes such as _“Lack of Input Validation,” “Lack of Patch Management,” “Security Misconfigurations,”_ and so on. This could come either under the “Executive Summary” or under a separate section beneath it.

Based upon this structure, let us look at a sample executive summary, taken from an actual pentest:

1. **Executive Summary**

Between the 4th and 20th of May 2023, HackHerWay conducted a comprehensive GreyBox web and network penetration test on Example CORP. Our objective was to gauge the security strength of the Example CORP network and their applications, identify potential vulnerabilities and evaluate the effectiveness of their current mitigation controls.

**Engagement Highlights**

* The domain is at _**“High Risk,”**_ failing below average compared to peers assessed with the same methodology.
* The overall security posture is low with critical vulnerabilities requiring remediation.
* Due to the absence of a _**Patch Management Policy**_, several public-facing portals were vulnerable which allowed HackHerWay to gain access to their internal network.

The findings from the penetration testing revealed that there were significant gaps in their security framework, especially concerning Critical/High-Risk vulnerabilities like Arbitrary File Uploads which can lead to unauthorized system access. Given the high-value nature of the affected application the absence of key protective controls is alarming.

Based on the findings presented in this report, Example CORP is at **High** risk which, is a higher-than-average rating compared to similar organizations assessed using the same testing methodology.

The vulnerabilities that were identified pose a significant business risk and demand urgent remedial action. Addressing these is paramount to prevent potential operational disruptions, financial losses, and or reputational damage. This report includes an in-depth analysis of all the vulnerabilities discovered, across your systems and network infrastructure. For ease of prioritization and response, we have classified these vulnerabilities into tiers: _**“Critical,” “High,” “Medium,”**_ and _**“Low.”**_
