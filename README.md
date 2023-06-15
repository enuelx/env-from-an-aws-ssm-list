![jest](https://github.com/github/docs/actions/workflows/test.yml/badge.svg)

# Create a dotenv from aws parameter store list

Create a dotenv from another dotenv file with a list of paths from aws parameter store

## Inputs

### `inputFilename`

Filename received as parameter or `.env.map` by default, in the root directory

### `outputFilename`
Filename received as parameter or `.env` by default, in the root directory

## Example input file

```sh
VAR1=/qa/core/var1
VAR2=/qa/core/var2
VAR3=/qa/core/var3
```

## Example output file

```sh
VAR1=value1
VAR2=value2
VAR3=value3
```

## Example usage

```yaml
name: Create dotenv file

on: [ push ]

jobs:
  create-dotenv-file:
    name: Create dotenv file
    runs-on: ubuntu-latest
    
    steps:
      - uses: actions/checkout@v3

      # reference documentation: https://github.com/aws-actions/configure-aws-credentials
      - name: Configure AWS Credentials
        uses: aws-actions/configure-aws-credentials@v2
        with:
          role-to-assume: arn:aws:iam::123456789100:role/my-github-actions-role
          aws-region: us-east-2
      
      - uses: enuelx/env-from-an-aws-ssm-list@v1
        with:
          inputFilename: '.env-ssm-paths' # Optional (default: '.env.map')
          outputFilename: '.env.development' # Optional (default : '.env')
```