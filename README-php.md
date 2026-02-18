# PHP updates

If the following error is seen after an update:

```json
{
  "name": "Internal Server Error",
  "message": "An internal server error occurred.",
  "code": 0,
  "status": 500
}
```

The culprit is likely incorrect permissions on `/var/lib/php/session`.
The fix is `chown -R craftcms:craftcms /var/lib/php/*`

Source:
`p-w-craftcms01:/root/.bash_history`

```shell
cd /var/lib/
ls -l
cd php
ls -l
chown -R craftcms:craftcms *
```
