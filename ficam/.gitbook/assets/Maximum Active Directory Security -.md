Maximum Active Directory Security - A Hacker's Guide to Protecting AD Domains and Networks



Introduction



I want to write a few words about this book and the manner in which it should be used. This book is not simply an instructional, or a "How-To" book. Its primary purpose is to get you started on a solid education in Active Directory Federal Identity, Credential, and Access Management (FICAM) managed domains and supporting network infrastructure. As such, it is probably constructed differently from any other computer book you have ever read.



Although this book cannot teach you everything you need to know firsthand, the references contained herein can; therefore, if you  very little about Active Directory domain and FICAM security, you will want to maximize the value of this book by adhering to the following procedure:



Each chapter (except for the early ones that set the stage) contains intermittent references that may point to whitepapers, technical reports, and other sources of solid, reliable information of substance (pertaining to the topic at hand). Those references appear in boxes that are labeled as XREF. As you encounter each source, stop for a moment to retrieve that source from the Internet. After you retrieve the source, read it, and then continue reading the book. Throughout this book, perform this operation whenever and wherever applicable. If you do so, you will finish with a very solid and basic yet foundational understanding of Active Directory domain and FICAM security.



I have constructed this book in this manner because Active Directory domain and FICAM network security is not a static field; it is dynamic and changes quite frequently and rapidly. Nonetheless, there are certain basics that every individual interested in security must fully grasp and understand. Those basics are not contained (in their entirety) in any one book (perhaps not even in dozens of them). The information is located on the Internet in the form of documents written by authoritative industry subject matter experts. These are the people who have either designed and developed native Active Directory infrastructure and architecture, who have actively threat hunted, discovered critical vulnerabilities within any one operating component of Active Directory, and published their findings with instructions for prevention and remediation, or are the individuals who have designed and developed security features that enhance the security posture of any one security control (administrative or technical) or policy implemented. The body of their work is vast, but each paper, Executive Order (EO), or technical journal or report is, at most, 40 pages in length (most are fewer than 10 pages).



To those readers who want only a casual education in Active Directory domain and FICAM network security may read the book without ever retrieving a single document from the Internet; however, if you are searching for something more, something deeper, you can obtain it by adhering to this procedure.



If you choose to use this book as a reference tool in the manner I have described, there are certain conventions that you need to know. If the resource you have been directed to is a tool, consider downloading it even if it is not for your specific platform. With a proper archive tool (like WinZip), you can extract the documents that accompany the distribution of that tool. Such documents often contain extremely valuable and supplemental information. For example, a popular scanner named SATAN (made expressly for Unix) contains security materials in HTML. These do not require you install Unix (in fact, all they require is a browser). Likewise, many other tools contain documents in PDF, TXT, DOC, PS, and other formats that are readable on many modern platforms available at the time of this writing.



=================================================================

**TIP:** SATAN is a special case. Some o the tutorials are in HTML but have `\*.PL` extensions. These extensions are used to signify documents that are written in Perl. If you do not have Perl installed, convert these documents to raw HTML. To do so, open them in a text editor such as Notepad++ and replace the first line (`<<HTML`) with `<HTML>`. Then rename the file with either an `\*.HTM`, or an `\*.HTML` extension. From that point on, your browser will load the pages perfectly.

=================================================================



Next, I need to say several things about the hyperlinks contained within this book. Each one was tested by hand. In certain instances, I have offered links overseas to papers that are also available here in the United States. This is because I tried to pick the most reliable links possible. By *reliable links*, I mean the links that are most easily retrieved n the shortest time possible. Although you wouldn't think so, some overseas links are much faster. Also, in some instances, I could only find a verified link to a document overseas (*verified links* means that when I tested the link, the requested item actually existed at the RUL in incidences of `Object Not Found` to practically nil. Naturally, however, your mileage will vary. Sites often change their structure, so expect a few links to be no longer valid (even though most were checked just a month or two before the book's printing).



Also, many hyperlinks are expressed in their totality, meaning that wherever possible, I have extracted the *total* address of an object and not simply the server on which it resides. In reference to downloadable files (tools, usually), these links will not bring you to a page. This will save you time, but might first be confusing to less experienced users. Don't be surprised when a dialog box appears, asking you to save a file.



At points throughout this book, whenever I specify what language or tool (or software application, or program) was written in, pay careful attention. Many tools mentioned herein require either a compiler or an interpreter before they can be built and used. If you do not currently have the language or interpreter necessary (or if your platform is different from that for which the tool was designed), re-examine the reference. Unless it seems that the distribution contains documents that are of value to you, you should probably refrain from downloading it. Moreover, many modern utilities come in source code form only. Although I have examined much of the source code myself, I cannot vouch for each and every line of it. If you intend to download source code and compile it on your own architecture, be aware that neither I or the publishers can be responsible or held liable for trojans or other malicious code that may exist in these files. The majority of files referenced are from reliable sources and many are accompanied by digital signatures on the packages, PGP keys, and other co-signing assurances of authenticity and integrity; however, code that has originated on cracker forums may or may not be clean. Those files, too, come with SHA digital signatures and should be ran against a SHA signature verifier to assert its claim of signature identity. Use you judgment in these instances.



=================================================================

**NOTE:** Special not to Windows and macOS users: if you have no idea what I am talking about, fear not. You will by the time you reach Chapter 6, "A Brief primer on TCP/OP." I made every possible attempt to make this book easily read and understood for all users of varying security skill levels. I have taken great pains to explain many terms and procedures along the way. If you ae already aware of the definitions, skip these passages. If you are not, read them carefully.

=================================================================



In reference to sites mentioned that I deem "very good," a word of caution: This is my opinion only. I classify sites as "good" if they impart information that is technically relevant, current, sound, or point you in many valuable directions. But simply because I say one site is good and say nothing about another does nt mean the other site is bad. I have hand-picked every site and each offer good information on security. Those I single out as particularly good are so identified usually because the maintainer of that site has done n exemplary job of presenting the information.



With respect to hyperlinks, I will say this: At the end of Appendix A, "Where To Get More Information," I offer an uncommented, bare list of hyperlinks. This is the equivalent of a huge bookmark file in your browser. There is a purpose for this which I discuss in detail within that particular Appendix, but I will briefly address that purpose now. That list is provided for serious students of security. By leading that list into a personal robot (Clearweb is one good example), you can build a huge security library or index on your local machine. Such personal robots rake the pages on the list, retrieving whatever file types you specify. For companies that have adequate disk space and are looking to build a security library, this can be done automatically. Most robots will clone a remote site within a few minutes.



Be aware, however, that the majority of links offered lead to webpages that may or may not contain many links themselves. Thus, if you are running such a robot, you'd better have adequate disk space for the output. Printed in their native form, all retrievable documents in that list (if retrieved with a root that goes out one level for each link) would print a stack of paper approximately seven feet tall. I know this because I have done it. In Appendix A, I describe the procedure to do so. If you decide to retrieve and print written information and binaries from all the sites listed, you will have the majority of written security knowledge available on the internet within two weeks. In organizations doing serious security research, this could have significant value, particularly if all documents are reformatted to a single file format (you could do special indexing and so forth).



Certain books or other documents have been referenced that are not available online. These documents are obtainable; however, in all cases, I have included as much information on them as possible. Sometimes, the ISBN or ISSN is included, and sometimes it is not. ISBNs were not always obtainable. In these instances (which are admittedly rare), I have included the Library of Congress catalog number or other, identifying features that may help you find the referenced material(s) offline. Any sources that could not be traced down (either on the Net or Dark Web) were omitted from the book.



Moreover, I have made every possible effort to give credit to individuals who have authored or otherwise communicated information that is of technical value. This includes postings in forums such as Reddit, Quora, and related sites. In almost all cases (with the exception of the list of vendors that appear in Appendix B, "Security Consultants," I have omitted the email addresses of the referenced parties. True, you can obtain those addresses by going to various sites, but I refrained from printing them within this book I have made every effort to respect the privacy of these individuals.



The list of vendors that appear in Appendix B















References:

\[1] https://artifex.com/blog/choosing-between-ghostscript-and-mupdf#:\~:text=like%20further%20information.-,Bitmap%20Output,input%20for%20display%20based%20use.

\[2] https://www.reddit.com/r/linux/comments/1r1h7r7/just\_used\_ghostscript\_today\_for\_the\_first\_time/

