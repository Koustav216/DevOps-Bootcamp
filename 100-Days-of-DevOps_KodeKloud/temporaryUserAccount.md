## Task
To setup a temporary user account with an expiry date.

## Solution
Use the following command:
```bash
sudo useradd -m -s /bin/bash -e YYY-MM-DD mark
```
After the given date i.e. **YYY-MM-DD**, the user can't login anymore.

To verify, we use
```bash
sudo chage -l mark # chage is short for change age
```
It shows the account aging information.

## Bonus
Also, we can modify the expiry date of an existing user by:
```bash
sudo chage -E YYY-MM-DD  mark # chage is short for change age
```
To set password expiry for an exising user:
```bash
sudo chage -m 7 -M 90 alice
```
- `-m` sets the minimum number of days that must pass before a password can be changed again.
- `-M` sets the maximum number of days a password is valid.

**Timeline:**
- Day 0: Password set

- Day 1–6: User cannot change password

- Day 7–89: User may change password

- Day 90: Last valid day

- Day 91: Forced password change on login

**Remember:**

- Account expiry controls whether the user can log in at all

- Password aging controls when the user is allowed or forced to change their password

---
### `usermod` command

`usermod` is the tool we use **after** a user exists.

`usermod` **modifies an existing user account** by editing:

* `/etc/passwd`
* `/etc/shadow`
* `/etc/group`
* `/etc/gshadow`

It does **not**:

* Create users
* Delete users


#### Change login shell

```bash
usermod -s /usr/sbin/nologin alice
```

Use cases:

* Convert a human into a service account
* Disable interactive access without deleting the user


#### Change home directory

```bash
usermod -d /new/home/alice -m alice
```

* `-d` → new home path
* `-m` → move existing files

Without `-m`, you strand files like abandoned luggage.


#### Lock / unlock the account

```bash
usermod -L alice   # lock
usermod -U alice   # unlock
```

Locking:

* Prepends `!` to the password hash
* Blocks password login
* **Does not** disable SSH key access


#### Add user to groups (this one ruins systems)

Correct:

```bash
usermod -aG docker,adm alice
```

Without `-a`, you **replace all supplementary groups**.
Congratulations, you just broke access across the system.

This is the single most common `usermod` footgun.

#### Important Gotchas

`usermod` does *not* handle

* SSH keys
* Cron jobs
* systemd user units
* Running processes

So:

```bash
usermod -L alice
```

Does **not**:

* Kill sessions
* Remove keys
* Stop jobs

You must handle those explicitly.

> `usermod` edits account metadata. It does not enforce behavior at runtime.

If a process is already running, `usermod` politely looks away.

