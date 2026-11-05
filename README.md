# Bug Bounty & Responsible Disclosure Program Policy

Chainflip Labs is committed to ensuring the security and integrity of the Chainflip Protocol. To achieve this goal, we invite security researchers and ethical hackers to participate in our Bug Bounty Program. This program encourages responsible disclosure of security vulnerabilities and provides incentives for those who help us identify and address such issues. By participating in our Bug Bounty Program, you agree to the following terms and conditions.

This document is the canonical version of the policy. Before submitting, please read it in full together with [KNOWN-ISSUES.md](./KNOWN-ISSUES.md), which lists behaviours that are deliberate design decisions or accepted risks and are not eligible for a reward.

## Scope of the Program

**Our Bug Bounty Program covers the following areas:**

- The Chainflip Protocol Code, including its Rust backend and solidity smart contracts.
- Public API endpoints and associated services operated by Chainflip Labs.
- chainflip.io operated web applications related to the protocol, including scan, swap, auctions, and validators.

Disclosures related to the above will be taken seriously, but only if they can be proven to be true. We have received many reports which assert a vulnerability without an accompanying proof of concept that meets the [evidence standards](#evidence-standards) below.

**Please note that this program does not cover:**

- Third-party applications or services.
- Third-party dependencies.
- The Chainflip website, domain, or email configuration, including DNS settings, DKIM, etc.
- Phishing vectors not related to the Protocol.
- Physical security or social engineering attacks.
- Denial of service (DoS) attacks. This includes ANY attack which causes service disruption until fixed but no financial benefit to the attacker (such as engine or node panics).
- Issues already reported by another researcher or identified internally.
- Deliberate design trade-offs and accepted risks listed in [KNOWN-ISSUES.md](./KNOWN-ISSUES.md).
- Scenarios that require a compromised or malicious governance key, aggregate key, or a supermajority of validators. These are trusted parties.
- Configuration or network exposure of nodes, Broker APIs or LP APIs run by third parties. Securing these is the operator's responsibility.
- Reorgs on external chains deeper than the configured safety margins, or transactions that reappear on an external chain after the deduplication window. Margins are chosen so that this is very unlikely, and it cannot be fully protected against.
- Documentation or code comment inaccuracies with no security impact.
- Findings that rely only on outdated or unofficial deployment recipes, testnets or development networks, unless the same issue affects mainnet.

You are welcome to contact us regarding these issues, but please note that we do not pay bounties for these kinds of reports.

## Before You Submit: Self-Check

Most submissions we receive are closed for one of a small number of reasons. Before sending a report, please check:

- [ ] I can show which release or runtime version contains the affected code, and whether it is live on mainnet or pending release.
- [ ] The trigger is plausible on mainnet, whether an attacker or an external condition, and does not require a trusted party (governance, aggregate key, validator supermajority) or an operator misconfiguration.
- [ ] The issue is not listed in [KNOWN-ISSUES.md](./KNOWN-ISSUES.md) or the out-of-scope list above.
- [ ] My proof of concept runs against the real Chainflip code and reaches the claimed impact.
- [ ] Every claim I make about code, documentation or on-chain state is accurate and cites its source.
- [ ] Someone gains funds, or something halts or needs manual intervention, and I can say who and what.

Optionally, you may find it useful to paste the following prompt into an AI assistant along with your draft report, this policy and KNOWN-ISSUES.md. This is offered as a help, not a requirement:

```text
You are reviewing a draft bug bounty report for the Chainflip protocol before submission.
Using the attached policy and KNOWN-ISSUES.md, check the report adversarially and answer:
1. Which release contains the affected code, and is it deployed on mainnet or pending release? What evidence does the report give?
2. What triggers the bug: an attacker, or an external condition? Is that trigger plausible on mainnet, and does it require any trusted party (governance, aggregate key, validator supermajority) or operator misconfiguration?
3. Is this a known issue or deliberate design listed in KNOWN-ISSUES.md?
4. Does the PoC run against the real code and reach the claimed impact, or does it rely on re-implementation, mocks or an argued downstream step?
5. Quote every factual claim about code, docs or on-chain state, and flag any you cannot verify against the cited source.
6. Who gains what, concretely? If no one gains funds and nothing halts, say so.
Conclude: submit, revise, or do not submit, with reasons.
```

## What a Valid Submission Must Contain

Submissions missing any of the following may be closed without assessment.

1. **Title.** One line describing the finding.
2. **Affected version.** The release or runtime spec version the bug affects, with evidence that the vulnerable code is live on mainnet or is pending release. Bugs in code that is not yet deployed are welcome, but say so explicitly: severity is assessed on the impact the bug would have once deployed.
3. **Trigger.** What causes the bug to occur. For an attack, who triggers it and what they need: keys, roles, funds, or control over an external chain or sequencer. For a bug that needs no attacker, the external condition that triggers it, for example oracle price volatility, witnessing falling behind, or a slowdown on an external chain.
4. **Preconditions.** Anything else that must be true, and how likely it is on mainnet.
5. **Impact.** What concretely happens: funds lost or frozen (whose, and roughly how much), a chain halt, or a need for manual intervention. State who profits.
6. **Proof of concept.** See [Evidence Standards](#evidence-standards).
7. **Suggested fix.** Optional.

The report goes in the email body in plain text. Attachments are allowed as supporting material only. A report that exists only as an attachment, or only behind an external link, will not be assessed until the essentials are in the body.

## Evidence Standards

- **Real code.** The proof of concept must run against the real Chainflip code: integration tests (for example `cf-integration-tests`), pallet tests that use the real runtime configuration, or a localnet. Standalone programs that "transcribe" or re-implement Chainflip logic are not accepted as proof.
- **Full path.** Mock-harness tests are accepted only if they reach the claimed impact. Showing an intermediate state and arguing that the impact is "one call downstream" is not enough.
- **Accurate claims.** Every claim about code, documentation or on-chain state must be accurate and verifiable. Reports with materially wrong claims are closed.
- **Documentation mismatches.** A mismatch between a code comment or document and the code's behaviour is not a vulnerability in itself. Report it as a normal GitHub issue unless it leads to real impact.
- **Severity.** Severity is assessed by Chainflip Labs against the criteria in this policy. Self-assessed severity is not taken into account.

## Responsible Disclosure

If you discover a potential security vulnerability, please report it to Chainflip Labs as soon as possible by following the responsible disclosure process outlined below:

1. Send an email to <security@chainflip.io> with the subject line "Bug Bounty Submission: [TITLE]", where [TITLE] is the one-line title of the finding.
2. Put the full report, containing everything listed under [What a Valid Submission Must Contain](#what-a-valid-submission-must-contain), in the email body.
3. Include any relevant code snippets, proof-of-concept scripts, or tools used to identify the vulnerability. Please conduct a proof of concept before submitting.
4. Include your contact information for us to reach out to you regarding the issue.
5. Please be patient while we review the submission.

## Submission Process

- **One finding per submission.** Separate findings must go in separate emails. Bundled reports may be returned unassessed.
- **Response times.** We aim to acknowledge submissions within 1 business day and to complete an initial assessment within 3 business days, depending on severity and workload. The full process, up to a payment decision, can take longer. Follow-ups sent before then will not be answered and do not speed up the review.
- **Clarification.** Chainflip Labs may ask one round of clarifying questions. Assessment decisions are final. Disagreements about scope or severity that repeat the original report will not get a further reply.
- **Repeat submissions.** Researchers who repeatedly submit out-of-scope, duplicate or inaccurate reports may be deprioritised or excluded from the programme.
- **Read the known issues first.** Please read [KNOWN-ISSUES.md](./KNOWN-ISSUES.md) and the out-of-scope list above before submitting.

## Rewards and Recognition

Chainflip Labs has rewarded several researchers over the years for their efforts and responsible disclosure.

Chainflip Labs will reward security researchers for responsibly disclosing security vulnerabilities based on the severity and impact of the issue. Rewards are provided at the discretion of Chainflip Labs.

To be eligible for a reward, a bug must be in code that is live on mainnet or pending release, and have real consequences: funds at risk, a network halt, or a need for manual intervention. It does not have to be triggerable by an attacker: a bug that is plausibly triggered by an external condition may also qualify. What does not qualify is a bug that can only be triggered by a trusted party.

The severity of the issue will be assessed according to expected impacts of the issue, using other similar programs as a baseline, though Chainflip will assess severity and corresponding reward size on a case by case basis.

Issues in which an attacker has no direct financial incentive to conduct the attack are automatically heavily downgraded in terms of their severity and impact, and are generally classed as out of scope, though there may be exceptions. Findings that are technically valid but have no realistic impact are acknowledged without a reward.

The first valid report of an issue wins. Issues that are already known internally, already reported by another researcher, or listed in [KNOWN-ISSUES.md](./KNOWN-ISSUES.md) are not eligible for a reward.

Rewards will be issued in FLIP tokens unless otherwise agreed upon with the researcher.

## Responsible Research

Researchers participating in the Bug Bounty Program must adhere to the following guidelines:

1. Do not engage in any activity that could disrupt Chainflip Labs' services or harm our users.
2. Do not access or modify data without proper authorization.
3. Do not disclose or publish any information related to vulnerabilities until they have been resolved by Chainflip Labs.
4. Comply with all applicable laws and regulations.

## AI Submissions

Due to the increased capabilities of frontier AI models, we are seeing an increase in the volume of submissions. Many submissions are clearly AI-written, and often extremely verbose, repetitive and unverified. Reviewing and responding to incorrect claims takes a lot of time away from development. For this reason, before submitting, please ensure that the report is accurate and succinct. The core claims should be clearly laid out along with a clearly-reasoned step by step proof of concept that meets the [evidence standards](#evidence-standards) above.

## Confidentiality

Chainflip Labs will treat all bug submissions and communication with researchers as confidential, except when disclosure is required by law. We encourage researchers to maintain confidentiality as well.

## No Legal Action

Chainflip Labs commits not to pursue legal action against security researchers who comply with the responsible disclosure guidelines outlined in this policy.

## Safe Harbour for Returning Assets

If any security researcher or ethical hacker should decide to exploit a found vulnerability to extract tokens or assets from the protocol in order to safeguard them from malicious parties, we strongly encourage that party to notify us immediately, and hereby confirm that our safe-return address for the Governance Council at Chainflip Labs is `0x38a4BCC04f5136e6408589A440F495D7AD0F34DB`.

Any party that sends safeguarded assets back to the Governance Council will be protected under no-legal-action rights and shall be rewarded for safeguarding exploitable assets.

## Program Changes

Chainflip Labs reserves the right to modify or terminate the Bug Bounty Program at any time without prior notice. We also reserve the right to adjust rewards and criteria.

## Contact

For any questions or to report security vulnerabilities, please contact us at <security@chainflip.io>

By participating in the Bug Bounty Program, you acknowledge that you have read and agree to these terms and conditions. Your cooperation in helping us improve our security is greatly appreciated. Thank you for contributing to the safety of our products and services.

Last updated: 5 November 2026
