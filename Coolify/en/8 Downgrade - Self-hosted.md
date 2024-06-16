[TOC]

A guide on how to downgrade the self-hosted version of Coolify.

If you have any issues with the latest version, you can simple downgrade to the previous version. Here is how you can do it:

- **Disable autoupdate**

Login as the `root` user (or any user that is in the `root` (initial) team), go to your `Settings` menu and disable the `Auto Update` feature.

- **Login to your server via SSH**

Login to your server via SSH and execute the following command:

```bash
  curl -fsSL https://cdn.coollabs.io/coolify/install.sh | bash -s 4.0.0-beta.277
```

Where `4.0.0-beta.277` is the version you want to downgrade to.

> Please note that downgrading could cause weird issues, as the database schema is not backward compatible. Some features might not work as expected.
