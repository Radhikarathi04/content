---
title: Testing a Content Security Policy
short-title: Testing
slug: Web/HTTP/Guides/CSP/Testing
page-type: guide
sidebar: http
---

<!-- DRAFT: structure only, prose to follow. -->

Deploying a {{Glossary("CSP", "Content Security Policy")}} to an existing site is rarely a single step.
A policy that is too strict will block resources the site depends on, and a policy that is too permissive provides little protection.
This guide covers the process of arriving at a policy you can enforce with confidence: testing it in report-only mode, collecting and interpreting violation reports, and deciding when it is safe to switch enforcement on.

This guide assumes you are already familiar with the concepts in [Content Security Policy (CSP)](/en-US/docs/Web/HTTP/Guides/CSP) and the individual [CSP directives](/en-US/docs/Web/HTTP/Reference/Headers/Content-Security-Policy).

## Report-only mode

<!-- The two headers, and running them together: enforce what is settled while testing the next revision. -->

## Setting up violation reporting

<!-- Reporting-Endpoints and report-to, the deprecated report-uri, browser support, and the choice between collecting reports yourself and using a third-party service. -->

## Understanding a violation report

<!-- Report fields and what they mean. Also what a report does not tell you: cross-origin blocked-uri values are coarsened, and source-file and line-number are often unhelpful for injected scripts. -->

## Distinguishing genuine violations from noise

<!-- Browser extensions, proxy and ISP injection, translation and accessibility tools, and third-party tags. How to filter each, and what a realistic signal-to-noise ratio looks like. -->

## Testing during development

<!-- Devtools console output, differences between development and production environments, and asserting the policy in automated tests so regressions are caught before deployment. -->

## Rolling out in stages

<!-- Introducing a policy incrementally by route or by proportion of traffic, and tightening directives one at a time rather than deploying a final policy immediately. Migrating from host allowlists to nonces or hashes. -->

## Constraints on large sites

<!-- Response header size limits and how they vary between servers and CDNs, truncation of long policies, and the interaction between per-request nonces and caching. -->

## Deciding when to enforce

<!-- What the reports should look like before switching from report-only to enforcement, and what to monitor immediately afterwards. -->

## Maintaining a policy

<!-- Handling new third-party requirements, and continuing to use report-only alongside an enforced policy to test the next revision. -->

## See also

- [Content Security Policy (CSP)](/en-US/docs/Web/HTTP/Guides/CSP)
- [CSP errors and warnings](/en-US/docs/Web/HTTP/Guides/CSP/Errors)
- {{HTTPHeader("Content-Security-Policy-Report-Only")}}
- {{HTTPHeader("Reporting-Endpoints")}}
- [Reporting API](/en-US/docs/Web/API/Reporting_API)
