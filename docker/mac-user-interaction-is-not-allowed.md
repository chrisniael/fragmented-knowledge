# Mac docker: User interaction is not allowed

```bash
docker login <url>
```

然后会提示

```bash
Username: shenyu
Password:
Error saving credentials: error storing credentials - err: exit status 1, out: `error storing credentials - err: exit status 1, out: `User interaction is not allowed.`
```

## 解决方案

```bash
security unlock-keychain
```

<https://github.com/docker/docker-credential-helpers/issues/82#issuecomment-367258282>
