# Ansible Role: uberspace-mail-forward

This is part of the uberspace roles collection.

This is meant to be used on your [Uberspace](https://uberspace.de/).

Please be aware, that I'm neither part of the Uberspace team, nor am I associated to them other than having some Uberspaces myself.
This project was created, because I wanted to use the roles for myself and thought they were okay-ish enough to share them.

## What is this (from the uberspace manual)

You can use forwardings in the form of $MAILBOX@$USER.uber.space. If you have set up additional domains, $MAILBOX@$DOMAIN will also work.

You can find the documentation of the replaced tool `uberspace mail user forward` in the Uberspace Manual [here](https://manual.uberspace.de/mail-forwarding.html).

## Notes

Each mailbox can only forward to one address. Setting the forward again, overwrites the existing one!

## Usage

| Variable | Choices/Default                            | Description                                                                                                                  |
| :------: | :----------------------------------------- | :--------------------------------------------------------------------------------------------------------------------------- |
|   user   |                                            | The mailbox user to use as catchall                                                                                          |
| address  |                                            | The mail address to forward to                                                                                               |
|  state   | <ul><li>present ✔</li><li>absent</li></ul> | "present" to enable the catchall, "absent" to disable it. Absent requires user to be set, present requries user and address. |
| forwards | []                                         | A list of user, address, state combinations to set multiple forwards at once                                                 |

## Examples

### Enable Farward

```yaml
- hosts: uberspace
  roles:
    - name: uberspace-mail-forward
      user: forwardme
      address: mail@allcolorsarebeautiful.example
```

### Disable Forward

```yaml
- hosts: uberspace
  roles:
    - name: uberspace-mail-forward
      user: dontforwardme
      state: absent
```

### Set multiple forwards

```yaml
- hosts: uberspace
  roles:
    forwards:
      - name: uberspace-mail-forward
        user: forwardme
        address: mail@allcolorsarebeautiful.example
      - name: uberspace-mail-forward
        user: dontforwardme
        state: absent
```
