# Security

Please report security problems privately to **TODO: security contact**, not in a public issue.

Include what you found, how to reproduce it and which version you use (ask your assistant to *"check the
connection to AI Knowledge Fabric"*; it shows the version and build).

## What the server does with your token

- It is entered only on the connect page, which the server shows on your own computer (`127.0.0.1`) under a
  one-time link. It never goes through the chat or to the AI model.
- It is saved on your computer: encrypted for your user account on Windows, in a file only you can read on
  macOS and Linux.
- It is sent only to the instance address saved with it, and never logged.
