# Apr 26 Hunting for Credentials and Building a Credential Type Reference Catalog

## Hunting for credentials and building a credential type reference catalog

Posted on Apr 26, 2020

Tags: [#red](https://embracethered.com/blog/tags/red) [#ttp](https://embracethered.com/blog/tags/ttp) [#book](https://embracethered.com/blog/tags/book) [#credentials](https://embracethered.com/blog/tags/credentials)

Adversaries are leveraging widely exposed clear text credentials to gain access to sensitive information.

At times the term “harvesting credentials” is used when red teamers emulate these attacks — which is something that appears to be more opportunistic and I would **propose that security teams start to actively hunt for credential exposure that can put their organization at risk** – in case you are not yet doing that.

### Actively hunting for credential exposure

The idea of **credential hunting is targeted and focused**, leveraging intelligence about systems and combing it with powerful search techniques to identify exposure.

Use the [Homefield Advantage](https://wunderwuzzi23.github.io/blog/posts/homefield-advantage/) to perform the best possible credential hunts.

### Credential Hunting Reference Sheet

Below is a reference sheet that I use for credential hunting during pentests. There is also a _csv_ version available on my github (see the references section on bottom):<br>

It’s nothing fancy — just a reminder on what kind of information to look for and build into tooling to make sure they are not exposed widely, or accessible by adversaries. There are more examples, tools and hunting techniques in my [Red Team Strategies book](https://www.amazon.com/gp/product/1838828869/ref=as_li_tl?ie=UTF8\&tag=wunderwuzzi-20\&camp=1789\&creative=9325\&linkCode=as2\&creativeASIN=1838828869\&linkId=07bfd6b729fbc2b2904160e0e16c337f) as well.

{% hint style="info" %}
VHD Files

**Bonus:** Hunting for virtual machine disk image files can be very fruitful in environments. They often contain loads of password hashes and other sensitive data.
{% endhint %}

## Goal: Building a public credential type reference catalog

**A goal would be to build a comprehensive open credential type reference catalog together for the industry. So tooling (for discovery and validation) for each type of credential can be built and is comparable with each other across tools and vendors.**

Let me know if this is something you are interested in building or working together on.

### References

* [Credentials Reference - Markdown](https://github.com/wunderwuzzi23/scratch/blob/master/creds.md)
* [Credentials Reference - CSV](https://github.com/wunderwuzzi23/scratch/blob/master/creds.csv)
* [Book: Cybersecurity Attacks - Red Team Strategies](https://www.amazon.com/gp/product/1838828869/ref=as_li_tl?ie=UTF8\&tag=wunderwuzzi-20\&camp=1789\&creative=9325\&linkCode=as2\&creativeASIN=1838828869\&linkId=07bfd6b729fbc2b2904160e0e16c337f)

***

Contact: [mailto:security@wunderwuzzi.net](mailto:security@wunderwuzzi.net) | Twitter: https://twitter.com/wunderwuzzi23 | GitHub: https://github.com/wunderwuzzi23 | YouTube: https://youtube.com/@embracethered

(c) WUNDERWUZZI 2018-2025

Disclaimer: Penetration testing requires authorization from proper stakeholders. Information on this blog is provided for research and educational purposes to advance understanding of attacks and countermeasures to help secure the Internet.

![](https://wuzzi.net/anamato/inc/rts.php?idsite=1\&rec=1)
