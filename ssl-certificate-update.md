---
layout: default
title: SSL Certificate Update
url: /ssl-certificate-update
previous: /security
next: /patterns
---

# SSL Certificate Updates

RubyGems 2.6.8 and newer have improved SSL error messages to help you diagnose
your problems.  Always make sure you download the latest released version.

**UPDATE 2014-12-21**: RubyGems 1.8.30, 2.0.15, and 2.2.3 have been released.
It requires manual installation, please see instructions [below](#installing-using-update-packages).

---

Hello,

You've probably reached this page after encountering the following SSL error when trying to
pull updates from RubyGems:

    SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed

This error is produced by changes in rubygems.org infrastructure. You can read the
[background below](#background). Please follow the instructions below to update your RubyGems:

## Installing using update packages

Now that RubyGems 2.6.x has been released, you can manually update to this version.

Download [the latest RubyGems](https://rubygems.org/pages/download)

Please download the file in a directory that you can later point to (eg. your
home directory, `~`, or the root of your harddrive, `C:\`)

Now, using your Command Prompt:

```
C:\>gem install --local C:\rubygems-update-2.6.10.gem
C:\>update_rubygems
```

After this, `gem --version` should report the new update version.

You can now safely uninstall `rubygems-update` gem:

```
C:\>gem uninstall rubygems-update -x
Removing update_rubygems
Successfully uninstalled rubygems-update-2.6.10
```

If this process does not work for you, you can try [manually adding the new certificate](#manual-solution-to-ssl-issue).

## Background

For those who are not familiar with SSL/TLS and certificates, there are
many parts involved in securely serving content.

SSL certificates are used on the website, which are obtained from a
certificate authority (CA) and generated from a private key, along with its
respective signature.

Previously, RubyGems' certificates used SHA-1 to provide a digest (or
checksum) of the private key without distributing the key itself
(remember, these need to remain private).

SHA-1 has been found to be weak, and a lot of websites have been
upgrading to the more secure SHA-2 (specifically SHA-256 or higher).

## Specific problem with RubyGems

The particular case with RubyGems (the command line tool) is that it has
to bundle the trusted certificates with the code. This allows RubyGems
to establish a connection with the servers even when the operating
system it is ran on does not have these certificates.

Previously, this certificate was provided by one Certificate Authority,
but the new certificate is provided by a different one.

Because of this, verions of RubyGems with both certificates were
released, in an attempt to simplify the change.

However, at the scale RubyGems operates at, it's impossible to make sure
everybody updates the software. There are also operating systems
shipping with old versions. As such, sometimes manual intervention (as
described above) is required.

This has been described on [Issue #1050](https://github.com/rubygems/rubygems/issues/1050#issuecomment-61422934)

We had discussed also on IRC, and patches and backports were provided to
all major branches of RubyGems: 1.8, 2.0, 2.2, and 2.4

You can find the commits associated with these changes here:

- [1.8 branch](https://github.com/rubygems/rubygems/commit/74ee66395c8e1b9ad6a45ba2f292bee8c6ea1a50)
- [2.0 branch](https://github.com/rubygems/rubygems/commit/98f5f44c7141881c756003e4256b1a96b200b98e)
- [2.2 branch](https://github.com/rubygems/rubygems/commit/17d8922966051864a0c4bf768623e9d0c854de26)
- [2.4 branch](https://github.com/rubygems/rubygems/commit/5a31f092d483ea7ccd91adbf08a88593cf0fbbc7)
- [2.6 branch](https://github.com/rubygems/rubygems/commit/5ee6a59784b1736553e16fda374c18491bb66abe)

Problem is, only RubyGems 2.4.4 got released, leaving Ruby installation with
1.8, 2.0 and 2.2 in a broken state.

Specially since RubyGems 2.4 is broken on Windows.

Please understand this could happen to anyone. Release multiple versions of
*any* software in a short span of time and be very time sensitive is highly
complicated.

Even if we have official releases of any of the versions that correct the
issue, it will not be possible install those via RubyGems (chicken-egg
problem described before).

Once official releases are out, installation might be simpler. In the
meantime, please proceed using the instructions described below.

## Manual solution to SSL issue

If the [above approach](#installing-using-update-packages) didn't
work for you, you can attempt to manually fix the problem by
adding the new trust certificate.

The steps are as follows:

- Step 1: Obtain the new trust certificate
- Step 2: Locate RubyGems certificate directory in your installation
- Step 3: Copy new trust certificate
- Step 4: Profit

### Step 1: Obtain the new trust certificate

We need to download the new trust certificate, [GlobalSignRootCA.pem](https://raw.githubusercontent.com/rubygems/rubygems/master/lib/rubygems/ssl_certs/index.rubygems.org/GlobalSignRootCA.pem).

Use the above link and place/save this file somewhere you can later find
easily (eg. your Desktop).

**IMPORTANT**: File must have `.pem` as extension. Browsers like Chrome will
try to save it as plain text file. Ensure you change the filename to end with
`.pem` after you have downloaded it.

### Step 2: Locate RubyGems certificate directory in your installation

In order for us copy this file, we need to know where to put it.

Depending on where you installed Ruby, the directory will be different.

Take for example the default installation of Ruby 2.1.5, placed in `C:\Ruby21`

Open a Command Prompt and type in:

```
C:\>gem which rubygems
C:/Ruby21/lib/ruby/2.1.0/rubygems.rb
```

Now, let's locate that directory. From within the same window, enter the path
part up to the file extension, but using backslashes instead:

```
C:\>start C:\Ruby21\lib\ruby\2.1.0\rubygems
```

This will open a Explorer window inside the directory we indicated.

### Step 3: Copy new trust certificate

Now, locate `ssl_certs` directory and copy the `.pem` file we obtained from
previous step inside.

It will be listed with other files like `AddTrustExternalCARoot.pem.`.

### Done!

You should now be able to install Ruby gems without issues now.

If you're still encountering issues, you can open an 
[issue on GitHub](https://github.com/rubygems/rubygems).
