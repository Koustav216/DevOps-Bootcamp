## WHAT
A **non-interactive user** is a user account that:

* **Cannot obtain a shell**
* **Cannot log in**
* Exists only to run services or own files

This is enforced via the **login shell** field.

### Where this is defined
In `/etc/passwd`, we might see:

```text
nginx:x:101:101:Nginx service:/var/lib/nginx:/usr/sbin/nologin
```

That last field is the key:

```text
/usr/sbin/nologin
```

or sometimes:

```text
/bin/false
```
Trying to log in using a non-interactive user, e.g.,

```bash
su - nginx
```

Gives the folloing result:

```text
This account is currently not available.
```

## Significance

Because production systems contain service accounts e.g.,

* `nginx`
* `postgres`
* `redis`
* `jenkins`
* `git`

These users:

* Own files
* Run processes
* Should never type commands

If a service is compromised:

* Attacker gets **no shell**
* No TTY
* No `.bashrc`
* No interactive escalation path

It’s damage containment.

These are used for:

* SFTP-only access
* Git over SSH
* Backup targets
* CI runners

Example:

```text
backup:x:2001:2001:Backup user:/data/backups:/bin/false
```
A non-interactive user can still run non-interactive shells via:

- systemd

- cron

- container runtimes

They just can’t log in like a human.
