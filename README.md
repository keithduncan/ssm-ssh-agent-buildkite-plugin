# ssm-ssh-agent-buildkite-plugin

Superseded by [iam-ssh-agent](https://github.com/keithduncan/iam-ssh-agent) which
improves security by removing the need for direct access to private key material.

---

Wraps the built-in Buildkite checkout phase in a one-shot SSH Agent, populated
with an SSH Private key fetched from the AWS Systems Manager Parameter Store.

Requires the awscli to be installed.

1. Add a [Deploy Key](https://developer.github.com/v3/guides/managing-deploy-keys/#deploy-keys)
to your GitHub repository.
1. Open the AWS Systems Manager Parameter Store console and create a
SecureString named `/github/{organisation}/{repository}/deploy-key` with the key.
1. Ensure your Buildkite agent has AWS IAM credentials with permission for
`ssm:GetParameter` and `kms:Decrypt`.

## Example

```yml
steps:
- command: script/cibuild
  plugins:
  - "keithduncan/ssm-ssh-agent#v1.0"
```
