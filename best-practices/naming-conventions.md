# Naming Conventions

A consistent naming convention makes resource ownership, environment, and purpose legible
at a glance — without it, every audit, cost report, and incident investigation starts with
manual detective work.

## General pattern

```
<resource-type>-<workload>-<environment>[-<region-short>]
```

Examples: `rg-platform-prod` (Azure resource group), `vpc-payments-prod` (GCP VPC),
`vnet-checkout-prod-eus2`, `sa-cicd-deploy` (service account, before its full email suffix).

## Azure prefixes

| Resource | Prefix |
|---|---|
| Resource Group | `rg-` |
| Virtual Network | `vnet-` |
| Subnet | `snet-` |
| Key Vault | `kv-` |
| Storage Account | `sa` (no hyphen — Azure restricts Storage Account names to alphanumeric only) |
| Managed Identity | `id-` |

## GCP prefixes

| Resource | Prefix |
|---|---|
| Project ID | `<business-unit>-<workload>-<environment>` (no fixed prefix; the pattern itself is the convention) |
| VPC | `vpc-` |
| Service Account | `sa-` |
| Cloud Router | `cr-` |

## Environment abbreviations

Use exactly these, consistently, everywhere (state keys, `.tfvars` filenames, CI job names, resource names): `dev`, `staging`, `prod`. Never mix in `development`, `stg`, `production` inconsistently across systems.

## Common mistakes

- Inconsistent abbreviation of environment names across different systems (Terraform state keys, resource names, CI job names).
- Omitting environment from a resource name, making it ambiguous during an incident which environment a resource belongs to.
- Encoding information that changes frequently (a team name that might reorg) into an immutable resource name instead of a mutable tag/label.

## Further Reading

- `best-practices/tagging-strategy.md`
- Companion repositories: `gcp-landing-zone` `docs/12-best-practices.md`; `terraform-enterprise` `docs/11-best-practices.md`
