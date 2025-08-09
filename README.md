# IAM Policy Audit Lab – Hands-On GRC with Terraform & Rego

## Scenario: The IAM Wildcard Panic

While reviewing a Terraform pull request, I spotted an IAM policy with `"Action": "*"` and `"Resource": "*"`.
This lab simulates catching and blocking such overly permissive policies before they reach production by using **Rego** and **Conftest**.

## Objective

Create a policy-as-code check that:

* Detects wildcard actions and resources
* Blocks risky IAM policies in CI/CD
* Maps technical enforcement to NIST 800-53 access control requirements

## Why It Matters

Wildcard permissions break least privilege, obscure accountability, and are a common root cause of cloud breaches. This lab enforces controls such as AC-2, AC-3, AC-4, and AC-6.

## How I Built It

1. **Simulated Terraform Output**
   Created `bad-policy.json` representing an insecure IAM policy.
2. **Wrote Rego Policy**
   `policy/iam.rego` denies any policy with `Action == "*"` or `Resource == "*"`.
3. **Tested with Conftest**
   Ran `conftest test bad-policy.json` to verify the detection.
4. **Automated with GitHub Actions**
   Added `.github/workflows/policy-check.yml` to run Conftest on every push and pull request.

## Key Takeaways

* Prevented high-risk IAM misconfigurations before deployment
* Learned and applied Rego for access control enforcement
* Integrated security checks directly into the development workflow
