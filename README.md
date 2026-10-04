# opensmtpd-table-ldap
Custom OpenSMTPD table to lookup and auth against LDAP.

Very simple POXIX shell implementation to allow OpenSMTPD to lookup users
against an LDAP server, and also to authenticate (K_AUTH). It uses
OpenBSD's `ldap` command to talk to the LDAP server.

Usage on smtpd.conf:

```
# Table definition
table myldap ldap

# Auth on subission port (outgoing mail)
listen on all port submission tls-require pki mail.example.com auth <myldap>

# Incoming mail lookup
action "remote_mail" lmtp "/var/dovecot/lmtp" rcpt-to virtual <myldap>
```
