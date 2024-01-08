
Request and set temporary credentials in a shell environment.


# Installation

install the `assume-role` script to somewhere in path.

# Configuration

Setup roles in `~/.aws/config` and `~/.aws/credentials` as documented in [AWS CLI userguide](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-role.html)

Example:

`~/.aws/config`

```bash
[profile management]
region=eu-central-1

[profile production]
role_arn=arn:aws:iam:123456:role/DeploymentRole
source_profile=management
mfa_serial=arn:aws:iam:633:mfa/jack   # optional
duration_seconds=3600                 # optional
external_id=abc123                    # optional
```

`~/.aws/credentials`

```bash
[management]
aws_access_key_id = ...
aws_secret_access_key = ...
```


# Usage

Execute a script `my-script` using temporary IAM credentials for production

```
$ assume-role production /path/to/my-script
```

This will set AWS\_ACCESS\_KEY\_ID, AWS\_SECRET\_ACCESS\_KEY and AWS\_SESSION\_TOKEN for duration of the script execution.

without a command, `assume-role` will output the credentials:

```
$ assume-role production
export AWS_ACCESS_KEY_ID="...."
export AWS_SECRET_ACCESS_KEY="..."
export AWS_SESSION_TOKEN="..."
```

you can store the credentials for your shell session by doing

```
$ eval $(assume-role production)
```

# Credits

This script aims to duplicate https://github.com/remind101/assume-role without support for windows PowerShell.
