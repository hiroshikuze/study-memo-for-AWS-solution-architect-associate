# CLAUDE.md — AI Assistant Guide

## Repository Overview

This is a Japanese-language personal study notes repository for the **AWS Certified Solutions Architect – Associate** exam. It is a pure Markdown documentation project with no code, build system, tests, or dependencies.

**Author:** hiroshikuze
**Language:** Japanese (content), English (README, commit messages)
**Purpose:** Personal reference notes focusing on easily-forgotten exam topics

---

## Repository Structure

```
.
├── README.md          # English intro, reference books/courses, sponsor links
├── index.md           # Japanese table of contents (main entry point)
├── compute.md         # EC2, Auto Scaling, API Gateway, ElastiCache
├── storage.md         # S3, EBS, EFS, Storage Gateway, Glacier
├── database.md        # Aurora, RDS for MySQL, Redshift, DynamoDB, DAX
├── network.md         # CloudFront, Route 53, VPC, ELB, Direct Connect, subnets
├── security.md        # KMS, CloudHSM, IAM (cross-references management.md)
├── cooporation.md     # SNS, SQS, SES (integration/messaging services)
├── analytics.md       # Kinesis, CloudWatch, CloudTrail, EMR
├── management.md      # CLI, IAM, Config, Organizations, STS, Trusted Advisor
├── automation.md      # CloudFormation, Elastic Beanstalk, OpsWorks, CodePipeline, ECS/EKS
└── other.md           # AWS Support plans (Basic, Developer, Business, Enterprise)
```

The `index.md` file is the canonical entry point and links to all topic files.

---

## Content Conventions

### Language
- All note content is written in **Japanese**
- File names, commit messages, and README headings are in **English**
- AWS service names appear in their original English form even within Japanese text

### Markdown Style
- Top-level heading (`# Title`) follows the pattern: `# <Topic>：AWSソリューションアーキテクトアソシエイト`
- AWS service names link to their official AWS Japanese documentation pages (e.g., `[Amazon EC2](https://aws.amazon.com/jp/ec2/)`)
- Comparison data is presented in Markdown tables using `|:---|:---|` alignment syntax
- Key terms or important warnings are **bolded** using `**text**`
- Lists use `*` bullets (not `-`)
- Two trailing spaces are used for line breaks within paragraphs

### Table Format
Tables follow this pattern:
```markdown
|種類|内容|
|:---|:---|
|項目A|説明A|
|項目B|説明B|
```

### Cross-references
Files cross-reference each other. Example: `security.md` defers IAM coverage to `management.md` with a link.

---

## Content Scope

Notes focus on **exam-relevant distinctions**, particularly:
- When to use one AWS service over another
- Pricing and billing nuances (e.g., Elastic IP costs, Reserved vs On-Demand)
- Limits and constraints (e.g., IAM: 5000 users/account, 10 groups/user)
- Encryption support per service
- Failover and high-availability behaviors
- Regional vs global service scope

Topics covered per file:

| File | Key Services |
|:---|:---|
| `compute.md` | EC2 instance types, Elastic IP, ENI, Auto Scaling, API Gateway, ElastiCache (Redis vs Memcached) |
| `storage.md` | S3 storage classes & consistency model, EBS volume types & encryption, EFS, Storage Gateway gateway types, Glacier retrieval tiers |
| `database.md` | Aurora auto-scaling, RDS failover/replication, Redshift clusters & Spectrum, DynamoDB, DAX |
| `network.md` | CloudFront CDN, Route 53 routing policies, VPC (flow logs, endpoints, peering), NAT/Internet gateways, ALB/NLB/CLB, Direct Connect |
| `security.md` | KMS vs CloudHSM, penetration testing policy |
| `cooporation.md` | SNS notification targets, SQS standard vs FIFO queues, SES |
| `analytics.md` | Kinesis variants, CloudWatch standard vs custom metrics, CloudTrail API logging, EMR |
| `management.md` | IAM (users, groups, roles, policies, STS), AWS Organizations, Config, Trusted Advisor, SWF, Active Directory integration |
| `automation.md` | CloudFormation (JSON/YAML templates, stacks), Elastic Beanstalk, OpsWorks (Chef/Puppet), CodeCommit/Build/Deploy/Pipeline, ECS/EKS/Fargate |
| `other.md` | Support plan tiers and feature comparison |

---

## Development Workflow

### No Build System
This repo has no package manager, linter, formatter, or CI pipeline. There is nothing to install or run.

### Making Changes
1. Edit the relevant `.md` file directly
2. Add new AWS services under the appropriate topic file
3. If a new topic category is needed, create a new `<topic>.md` file and add a link to `index.md`
4. Update `README.md` only for structural changes (new references, sponsorship, etc.)

### Commit Messages
Historical commits use short English imperative messages:
- `"Add subnet."`
- `"Update document."`
- `"Update documents."`
- `"Genre decomposition."`

Follow the same terse, English, imperative style.

---

## Key Conventions for AI Assistants

1. **Write note content in Japanese** — all body text follows the established Japanese style
2. **Preserve the heading format** — `# <Category>：AWSソリューションアーキテクトアソシエイト` for top-level headings in topic files
3. **Use official AWS JP doc links** — link service names to `https://aws.amazon.com/jp/<service>/` where possible
4. **Keep notes concise** — this is exam prep, not a tutorial; favor bullet points and tables over prose
5. **Bold critical distinctions** — use `**text**` for exam-critical caveats (e.g., what a service cannot do)
6. **No code blocks** — this is a notes repo; avoid adding code examples unless strictly needed for CLI commands
7. **Maintain cross-references** — if a topic is covered in another file, link to it rather than duplicating content
8. **Do not add English prose** — even if editing, keep body content in Japanese to match the established style
9. **Typos in file names** — `cooporation.md` (not `cooperation.md`) is an existing file name; do not rename it without updating `index.md` and all cross-references
