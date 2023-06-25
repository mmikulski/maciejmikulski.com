+++
title = "How to reclaim disk space taken over by WSL"
slug = "how-to-reclaim-disk-space-taken-over-by-wsl"
date = 2023-05-14

+++

Partitions used by the WSL distro on Windows are dynamically extended when you need more space for them. Unfortunately it doesn't work the othey way round. Ie. when you clean them up (by removing `node_module` folders from your experimental repos ;) ) Windows will not scale them down and you'll wonder where did all of the space go.

Fortunately there's a way to do it yourself.

1. Shutdown the WSL. (You may also need to to shutdown the Docker Desktop which will try to restart the WSL.)
```
wsl.exe --shutdown
```

2. Call Optimize-VHD commandlet pointing it to the file representing the WSL partition on windows file system.
```
Optimize-VHD -Path %PROFILE%\AppData\Local\Packages\CanonicalGroupLimited.Ubuntu20.04onWindows_79rhkp1fndgsc\LocalState\ext4.vhdx -Mode Full
```

If you want to check how much space the distro uses atm:
```
wsl.exe --system -d Ubuntu df -h /mnt/wslg/distro
```

Cheers!

Bibliography
# https://superuser.com/questions/1606213/how-do-i-get-back-unused-disk-space-from-ubuntu-on-wsl2
# https://learn.microsoft.com/en-us/windows/wsl/disk-space

