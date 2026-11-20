---
tags: [werkwijze, claude, systemd]
---
# claude-remote-control

Systemd-service die `claude remote-control` laat draaien (User almalinux, werkmap `/srv/docker/reismannetje`, in `script` voor een pty, `Restart=always`). Hierdoor werken de mobiele/web-sessies van [[Claude Code sessies]].

Als sessies op "thinking" blijven hangen: eerst `systemctl status claude-remote-control`. Zie [[Systemd-services]].
