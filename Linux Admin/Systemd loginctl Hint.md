<!-- permalink: 2e770ccb575c4f49136e675dc0965083 DO NOT DELETE OR EDIT THIS LINE -->
# systemd loginctl Hint

If you need a user's processes to continue after a user session terminates, you can run `loginctl enable-linger <username>`

This is useful for things like podman containers running outside of an ssh session, for example. This is even required when you have a systemd service set up for podman-compose.