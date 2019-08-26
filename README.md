# Introduction

Using mutt (or pine), but annoyed that it doesn't give you any
notifications when you've received new emails? buzz-ed is a simple
application that detects new emails on IMAP servers using IDLE (push
rather than pull). When it detects unseen messages, it shows writes 
the amount of new messages to a defined file and runs a defined command.

This project is a Rust fork of
[hasmail](https://github.com/jonhoo/hasmail), which provides basically
the same features, and is written in Go.


# Configuration

buzz-ed looks for a
[TOML](https://github.com/toml-lang/toml#user-content-example)
configuration file in `~/.config/buzz/buzz.toml` on startup. The
configuration file consists of a number of sections, each corresponding
to one account:

```toml
[gmail]
server = "imap.gmail.com"
port = 993
username = "jon@gmail.com"
pwcmd = "gnome-keyring-query get gmail_pw"
```

## Running buzz-ed

```
buzz /tmp/mails "pkill -RTMIN+2 i3blocks"
```

The first argument is the file, where it stores the amount of unread messages.
The second argument is the script or programm it starts after the amount has changed.


## Account fields

The value in `[]` can be anything (though avoid `.` as it will be parsed
as a new TOML section). The options for an account are as follows:

 - `server`: The address to connect to. MUST currently be SSL/TLS
   enabled.
 - `port`: The port to connect to.
 - `username`: Username for authentication.
 - `pwcmd`: Command to execute to get password for authentication.


