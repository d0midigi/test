# 4.1 How Federal Cybersecurity Authority Flows

## 4.1 How Federal Cybersecurity Authority Flows

Federal cybersecurity does not operate through a single chain of command.

That is one of the first things a technically oriented practitioner has to understand.

There is a tendency to search for one document that answers the question, _What are we required to do?_ For a federal Active Directory environment, that document usually does not exist.

The actual answer may require several layers of authority.

A statute may establish the federal obligation to maintain an information-security program. NIST standards and guidance may provide the risk-management structure and technical control framework. OMB may establish government-wide implementation or reporting direction. A departmental issuance may specify how those requirements apply within the Department of Defense. DISA technical guidance may translate portions of them into platform-specific configuration requirements. An Authorizing Official may accept residual risk associated with implementation. The local command may establish procedures necessary to operate that implementation safely within its mission environment.

The directory engineer sees the final configuration.

The configuration may therefore be several layers removed from the authority that caused it to exist.

Understanding this structure prevents two common errors.

The first is treating every federal cybersecurity document as though it possesses the same authority.

A NIST Special Publication, a FIPS standard, an OMB memorandum, a DISA STIG, a CISA Binding Operational Directive, a DoD Instruction, and a local standard operating procedure do not occupy interchangeable positions in the governance architecture. Their applicability, issuing authority, audience, and implementation purpose differ.

The second error is the opposite: assuming that because a high-level policy does not specify an Active Directory registry value, group permission, or Kerberos setting, it has no technical meaning.

High-level requirements are not supposed to configure Domain Controllers.

They establish outcomes, responsibilities, constraints, or risk expectations that must eventually be engineered.

The work of cybersecurity governance is the translation between those layers.
