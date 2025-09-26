# llm-snippets

A collection of LunarVim LuaSnip snippets for various development tasks.

## Terraform Snippets

**Location**: `snippets/terraform.lua`

### Available Triggers

| Trigger | Description |
|---------|-------------|
| `tfaws` | AWS provider block with region |
| `tfaws_profile` | AWS provider block with region and profile |
| `tfreqp_aws` | Terraform required_providers block for AWS |
| `tfbackend_s3` | S3 backend configuration |
| `tfterraform_backend_s3` | Complete terraform block with S3 backend |
| `tfaws_all` | Full setup: terraform + required_providers + S3 backend + AWS provider |
| `tfvar` | Variable definition template |
| `tfout` | Output definition template |
| `tfres` | Generic resource template |
| `tfdata` | Generic data source template |
| `tfmod` | Module block with version |
| `tflocals_tags` | Common tags locals block |

### Default Values

- **AWS Region**: `ap-northeast-2`
- **S3 Backend Bucket**: `dealertire-terraform-state-bucket`
- **S3 Backend Key**: `tirepick-prod/database/terraform.tfstate`
- **AWS Provider Version**: `5.99.1`
- **Project Tags**: `tirepick` (Project), `prod` (Environment)

### Usage Examples

#### Complete Terraform Setup (`tfaws_all`)
Generates a complete Terraform configuration:
```hcl
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "5.99.1"
    }
  }
  backend "s3" {
    bucket       = "dealertire-terraform-state-bucket"
    key          = "tirepick-prod/database/terraform.tfstate"
    region       = "ap-northeast-2"
    encrypt      = true
    use_lockfile = true
  }
}

provider "aws" {
  region = "ap-northeast-2"
}
```

#### S3 Backend Only (`tfbackend_s3`)
Generates just the S3 backend configuration:
```hcl
backend "s3" {
  bucket       = "dealertire-terraform-state-bucket"
  key          = "tirepick-prod/database/terraform.tfstate"
  region       = "ap-northeast-2"
  encrypt      = true
  use_lockfile = true
}
```

### Installation

1. Copy `snippets/terraform.lua` to your LunarVim snippets directory:
   ```bash
   cp snippets/terraform.lua ~/.config/lvim/snippets/
   ```

2. Ensure LunarVim loads local Lua snippets by adding this to your `config.lua`:
   ```lua
   require("luasnip.loaders.from_lua").lazy_load({ paths = "~/.config/lvim/snippets" })
   ```

3. Open a `.tf` file in LunarVim, type a trigger (e.g., `tfaws_all`), and press Tab to expand the snippet.
