# Linux Basics for Cybersecurity & Penetration Testing (Kali Linux)

This guide is meant to teach you Linux **from a practical, security-focused perspective**. Every part explains **what it is, why it matters for pentesting, and gives you something to try**.

---

## Why Linux Matters

If you want to break into pentesting or cybersecurity, Linux is where almost everything happens. Servers run Linux. Tools run on Linux. Exploits assume you understand Linux. If you don’t get the OS, you won’t understand the attacks.

**Try this:** Open a terminal in Kali and run:

```bash
whoami
uname -a
```

Notice your user and system version. These simple commands show who you are and what system you’re on — critical info for attacks and defenses.

References:

* [Kali Docs](https://www.kali.org/docs/)
* [Debian Docs](https://www.debian.org/doc/)

---

## The Linux Filesystem

Linux has one tree, starting at `/`. No drive letters. Understanding this is critical because files, configs, and logs are everywhere, and attackers need to know where to look.

### Important Directories

* `/etc` – configs like passwords, services, SSH keys. Check `ls -la /etc`.
* `/home` – user files, scripts, keys. Try `ls -la /home`.
* `/root` – root user’s files. You usually shouldn’t be here unless escalating.
* `/var/log` – logs. Look here to see what’s recorded.
* `/tmp` – temporary files. Often abused in attacks.

**Try this:** Search for all `.conf` files in `/etc`:

```bash
find /etc -name "*.conf" 2>/dev/null | head
```

Reference:

* [FHS Standard](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html)

---

## Users, Groups, and Privileges

Linux is multi-user. Permissions control everything.

* Regular users can’t touch everything. Root can.
* Groups define what multiple users can do.
* Sudo lets you run commands as root safely.

**Try this:**

```bash
id
groups
sudo -l
```

Look at what sudo allows you to do — that’s your potential attack surface.

Reference:

* [Linux Users Guide](https://www.tldp.org/LDP/intro-linux/html/sect_07_01.html)
* [GTFOBins](https://gtfobins.github.io/) (examples of sudo exploitation)

---

## File Permissions

Permissions are at the heart of Linux security. They define who can read, write, or execute a file.

Check permissions:

```bash
ls -l /usr/bin
```

Find world-writable files (can be abused):

```bash
find / -perm -002 2>/dev/null
```

Find SUID files (run as owner, often root):

```bash
find / -perm -4000 2>/dev/null
```

Reference:

* [Permissions Explained](https://wiki.archlinux.org/title/File_permissions_and_attributes)

---

## Package Management (APT)

APT installs and updates software. Outdated or untrusted packages are a security risk.

Update your system:

```bash
sudo apt update && sudo apt full-upgrade -y
```

Install a tool:

```bash
sudo apt install nmap wireshark -y
```

**Try this:** List installed packages and pick one to research for vulnerabilities:

```bash
dpkg -l | less
```

Reference:

* [APT Docs](https://wiki.debian.org/Apt)

---

## Processes and Services

Every process is a potential point of compromise.

* List processes: `ps aux | less`
* Interactive: `top` or `htop`
* Check services: `systemctl list-units --type=service`
* Check network: `ss -tulpn`

**Try this:** Identify a service running as root and consider what could happen if it’s exploited.

References:

* [proc Filesystem](https://man7.org/linux/man-pages/man5/proc.5.html)
* [Systemd](https://www.freedesktop.org/wiki/Software/systemd/)

---

## Environment Variables

Variables affect how programs run. Misconfigurations can be exploited.

Check them:

```bash
printenv
```

**Try this:** Add a directory to your `PATH` and see how command resolution changes.

Reference:

* [Bash Variables](https://www.gnu.org/software/bash/manual/)

---

## Kali-Specific Notes

* Many tools require `sudo`
* Rolling release – update often
* Snapshot your VM before experiments

**Try this:** Take a snapshot, break something, then roll back. Understand safe experimentation.

Reference:

* [Kali Rolling Release](https://www.kali.org/docs/general-use/kali-linux-rolling/)

---

## Ethics

Use these skills responsibly. Only run tools on machines you own or have permission to test.

Reference:

* [Kali Legal Guidelines](https://www.kali.org/docs/legal/)

---

## Next Steps

* Linux Networking basics
* File permissions & privilege escalation
* Bash scripting for pentesting
* Security tool practice (Nmap, Metasploit, Wireshark)

This guide is your foundation. Every command, directory, and concept here is a stepping stone toward **understanding how attackers think and how defenders secure systems**.
