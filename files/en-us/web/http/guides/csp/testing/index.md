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
This guide covers the practical side of arriving at a policy you can enforce with confidence: refining it iteratively using violation reports, working out which reports matter, and deciding when it is safe to switch enforcement on.

The [Content Security Policy (CSP)](/en-US/docs/Web/HTTP/Guides/CSP) guide describes report-only mode and how to set up violation reporting.
This guide assumes you have those in place.

## Distinguishing genuine violations from noise

<!-- Browser extensions, proxy and ISP injection, translation and accessibility tools, and third-party tags. How to filter each, and what a realistic signal-to-noise ratio looks like. -->

## Rolling out in stages

A policy is rarely correct on the first attempt.
A practical approach is to deploy a draft policy in report-only mode, collect violations over a representative period, and then refine the policy directive by directive.

Start with the directive generating the highest volume of violations.
High volume usually indicates either a resource the site genuinely depends on, or a directive that has been drawn too narrowly.
Adjust the policy, deploy again, and continue monitoring.
Working through one directive at a time makes it easier to attribute a change in violation volume to a specific edit, though several can be adjusted together once you are confident about what a group of reports represents.
Repeat until the remaining violations are ones you understand.

How long to spend in report-only depends on the traffic the site receives and on how much of it is seasonal or campaign-driven.
The first refinements tend to be obvious within a few days, since the highest-volume directives show up quickly.
Allowing a further period after that is useful, because lower-frequency violations only appear once the site has been exercised by a representative range of users, devices and journeys.

Violation reports can be collected by any endpoint that accepts them.
On larger sites they are often routed into an existing observability or monitoring platform alongside other telemetry, which makes it easier to track volume over time and to compare one deployment against the next.

<!-- TODO: migrating from host allowlists to nonces or hashes. -->

## Constraints on large sites

<!-- TODO: response header size limits, and the fact that they vary between servers and CDNs. -->

<!-- TODO: the policy the browser enforces is not necessarily the policy the server sent. Intermediaries such as CDNs, proxies and security products can rewrite or truncate headers in transit, so when console errors do not match the configured policy, check the actual response header in the network panel first. Where an intermediary is responsible, resolution may be outside your control; verify from the browser rather than relying on a report that a change has been deployed, since edge configuration often rolls out gradually and by region. -->

<!-- TODO: interaction between per-request nonces and caching. -->

## Deciding when to enforce

<!-- What the reports should look like before switching from report-only to enforcement, and what to monitor immediately afterwards. -->

## Living with an enforced policy

Enforcing a policy is not the end of the work.
Once a policy is enforced it becomes a constraint on every future change to the site, and it needs to be maintained alongside the code it protects.

Three situations come up repeatedly.

**New third-party integrations.**
Adding an embed, a tag manager, an analytics provider or a payment widget will usually require a corresponding change to the policy before it will load.
It is worth treating the policy change as part of the work of adding the integration rather than as a follow-up, so that the integration is not merged in a state where it is silently blocked.

**Exceptions granted during rollout.**
Refining a policy often involves temporarily allowing a source in order to unblock a release, with the intention of narrowing it later.
These exceptions are easy to forget, and each one weakens the policy for as long as it remains.
Recording why an exception was added, and revisiting them periodically, keeps the policy from drifting back towards being permissive.

**Changes to the page itself.**
An enforced policy can be broken by changes that have nothing to do with security.
Redesigning a page, replacing a component, or moving content to a different origin can all introduce a resource the policy does not allow, and code review will not usually catch it because the change looks unrelated to the policy.
Violations of an enforced policy are still reported if a reporting endpoint is configured, so it is worth continuing to monitor reports after enforcement rather than only during rollout.

> [!NOTE]
> Because a violation of an enforced policy blocks the resource, the first sign of a problem is often a broken feature rather than a security alert.
> Keeping reports visible to the team that owns the page, rather than only to the team that owns the policy, shortens the time it takes to connect the two.

## See also

- [Content Security Policy (CSP)](/en-US/docs/Web/HTTP/Guides/CSP)
- [CSP errors and warnings](/en-US/docs/Web/HTTP/Guides/CSP/Errors)
- {{HTTPHeader("Content-Security-Policy-Report-Only")}}
- {{HTTPHeader("Reporting-Endpoints")}}
- [Reporting API](/en-US/docs/Web/API/Reporting_API)
