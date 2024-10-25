# rsc.io/mailgun

This repo holds basic utilities for interacting with the
[Mailgun email service](https://www.mailgun.com).

`rsc.io/mailgun/cmd/mailgun-mail` is a drop-in replacement for the mail-sending mode of BSD mailx.

`rsc.io/mailgun/cmd/mailgun-sendmail` is a drop-in replacement for the mail-sending mode of the sendmail daemon.

The idea behind both these programs is that you can install them in
place of the usual mail and sendmail programs, and then programs can 
still send mail from your local system, without having to configure and
run a full-blown mail system.

# Instructions

To prevent GLIBC errors when deploying binary to a different machine prior to compiling run

```terminal
export CGO_ENABLED=0
```

To compile

```terminal
go build -o bin/mailgun-sendmail ./cmd/mailgun-sendmail
```

Place primary domain key in `/etc/mailgun.key` with the format:

```
domain.tld api:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

Place additional domain keys as example  `/etc/mailgun.mydomain.key` with the same format:

```
mydomain.tld api:xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
```

To send using a different domain key specify with the `-K` flag

```
mailgun-sendmail -K '/path/to/mailgun.mydomain.key'
```
