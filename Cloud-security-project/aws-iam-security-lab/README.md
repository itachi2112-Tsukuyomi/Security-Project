AWS IAM Security Lab – Evidence-Based Implementation
Project Overview

This repository documents a hands-on AWS IAM security lab focused on least privilege, privilege escalation via iam:PassRole, and proper remediation.

The project is intentionally evidence-driven, using:

Real AWS console screenshots

Real IAM policy JSON files

Clear separation between misconfiguration and fix

The goal is to demonstrate how IAM vulnerabilities occur in real environments and how they are correctly mitigated.

Repository Structure
aws-iam-security-lab/
├── screenshots/
├── policies/
├── docs/
└── README.md

Screenshots and What They Demonstrate

All screenshots are taken from a real AWS account and validate the security controls implemented in this lab.

1. IAM Users and Separation of Duties

File

screenshots/iam-users-overview.png


Demonstrates

Separate IAM users for development and security auditing

Group-based access control (RBAC)

MFA enabled on IAM users

No direct user-attached policies

2. Developer Access Denial (Least Privilege Validation)

Files

screenshots/dev-user-iam-access-denied.png
screenshots/dev-user-ec2-access-denied.png


Demonstrates

Developer cannot list IAM users, MFA devices, or access keys

Developer cannot enumerate EC2 account-level metadata

Reconnaissance and enumeration are blocked

Access denial confirms that least privilege is enforced correctly.

3. Developers Group Policy Attachment

File

screenshots/developers-group-policy-attach.png


Demonstrates

IAM permissions are applied at the group level

The PassRole policy is actively attached and enforced

The configuration is operational, not theoretical

4. Vulnerable iam:PassRole Policy (Attack Simulation)

File

screenshots/vulnerable-passrole-policy.png


Demonstrates

iam:PassRole configured with a wildcard resource ("*").

Ability for a low-privilege identity to pass any IAM role to AWS services

A real-world privilege escalation condition

This configuration is intentionally insecure and used only for learning and analysis.

5. Fixed iam:PassRole Policy (Remediation)

File

screenshots/fixed-passrole-policy.png


Demonstrates

Role passing restricted to a single least-privileged role

Reduced blast radius

Prevention of privilege escalation

6. Security Auditor Read-Only Visibility

Files

screenshots/sec-auditor-policy-view.png
screenshots/sec-auditor-cloudtrail.png


Demonstrates

Read-only visibility into IAM policies and roles

Ability to review CloudTrail logs

No permissions to modify or delete resources

This enforces separation of duties and supports incident response and forensic analysis.

7. Password Policy (Baseline Security Control)

File (optional baseline)

screenshots/password-policy.png


Demonstrates

Centralized IAM password policy

Basic credential hygiene enforcement

IAM Policies Used in This Project

All IAM policies are stored as code in the policies/ directory.

1. Developer Least Privilege Policy

File

policies/least-privilege-policy.json


Purpose

Allow developers to view infrastructure

Prevent any modification actions

Block IAM access entirely

2. Vulnerable PassRole Policy (Intentional Misconfiguration)

File

policies/vulnerable-passrole-policy.json


Purpose

Simulate a real-world IAM misconfiguration

Demonstrate indirect privilege escalation paths

Used only for attack analysis

3. Fixed PassRole Policy (Secure Configuration)

File

policies/fixed-passrole-policy.json


Purpose

Restrict role passing to a single safe role

Maintain required functionality

Eliminate escalation risk

4. EC2 Role Trust Policy (Reference)

File

policies/ec2-role-trust-policy.json


Purpose

Defines which AWS service (EC2) can assume the role

Critical to understanding PassRole exploitation paths

Key Security Takeaways

IAM attacks often occur through indirect permission paths

iam:PassRole is one of the most dangerous IAM permissions

Blocking enumeration does not prevent exploitation

Least privilege must include role-passing controls

Security auditing must be independent and read-only

Project Status

IAM users and groups implemented

Real IAM misconfiguration simulated

Proper remediation applied

Evidence captured via screenshots

Enterprise-style documentation completed