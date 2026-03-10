# Contributing

Thanks for considering a contribution! This is a small project so the process is lightweight.

## Reporting Issues

Open an issue on GitHub with:
- Your CopyQ version (`copyq --version`)
- Your qrencode version (`qrencode --version`)
- Your OS and platform
- What you expected vs what happened
- Any error output from running `copyq` in a terminal

## Submitting Changes

1. Fork the repo and create a branch
2. Make your changes to `qrcode-commands.ini`
3. Test by importing the commands into CopyQ:
   ```bash
   # Remove old commands
   copyq eval 'var c = commands(); var keep = []; for (var i = 0; i < c.length; i++) { if (String(c[i].name).indexOf("QR Code") < 0) keep.push(c[i]); } setCommands(keep);'

   # Import your version
   cat qrcode-commands.ini | copyq eval 'var nc = importCommands(input()); var e = commands(); for (var i = 0; i < nc.length; i++) e.push(nc[i]); setCommands(e);'
   ```
4. Verify all submenu items work (generate to clipboard, save to file, configure)
5. Open a PR with a short description of what you changed and why

## Things to Keep in Mind

- CopyQ 9.0+ is the minimum supported version
- The commands use `settings()` for config persistence — don't break existing user settings
- Keep the INI format compatible with `importCommands()` — use the `[Commands]` format with numbered keys
- Test on your platform and note which OS you tested on in the PR

## Ideas Welcome

If you have an idea but don't want to implement it, feel free to open an issue to discuss.
