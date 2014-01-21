ExtensionWatch Database
=======================

This repo is a database of extensions to ban, domains to monitor, and so on.  It is publicly viewable and maintained to keep everyone honest.

Why do it this way?
-------------------

I thought about building out a full web service with Sinatra/Rails, but then I hit on a few reasons why this will work better:

* **It's simpler.**  I don't have to worry about the app going down in the middle of the night and people yelling about it.  I build one JSON file, serve it from a CDN (currently GitHub Pages), and that's that.  This may not scale depending on the amount of malware that starts showing up, but it's perfect for now.
* **It's more open.** Having the entire contents of the database open for all to see means that there can't be any accusations of favoritism, secret banning, and so on.  The JSON files in this repo are built into the single `database.json` file that the ExtensionWatch extensions consume, which are also publicly viewable in the companion repository for the website.
* **It's more collaborative.** I don't have to train anyone to use some ridiculous web app to tell us about malware.  If you know how to use GitHub, you can report malware.  Even better, there can be a totally open discussion about it, whether it's actually malware, whether a straight blacklisting is in order or simply a domain alert, and so on.  Then we can link those discussions from the blacklist entry so if there's any discrepency, the discussions that lead to the entry can inform it.

The last one is really the big one.  The workflow I've devised should limit most concerns about "who's watching the watchers" since the discussions leading to adding an extension are open.

Workflow
--------

To report a malware/adware extension, create an issue with:

* Title it with the extension name
* The extension's ID or installation domain or link or something we can identify it with
* As much information about the malware it's peddling as possible (ad networks being used, malicious activities performed, etc.).  We will verify all this information, but the the more we have to work with at the beginning, the better.

At that point, once it's greenlit by someone, create a PR with the JSON file in place and mention the issue in the PR body.  We'll merge it in and on the next deploy, the extension(s) will pull down the new data and start using it immediately.

To report a domain/IP that's peddling bad things, create an issue with: 

* Title it with the domain or address
* As much information about the malware it's peddling as possible (ad networks being used, malicious activities performed, etc.).  We will verify all this information, but the the more we have to work with at the beginning, the better.
* A list of extensions using it.

The process is pretty much the same after that.

If you're wanting to work on more forensic analysis type things (e.g., looking for malicious DOM additions in pages), do that in the extension-specific repo.  Those concerns have to be addressed on a per-browser basis since they all have different restrictions.

What is "malware"?
------------------

The term "malware" is somewhat fluid, but here's the definition we're using here:

> Any piece of software that behaves in an intrusive or hostile manner.

This includes directly damaging stuff like viruses, password strealers, and so on, but it also includes more innocuous but no less intrusive things like unwanted adware.  If you're iffy about whether the behavior you're seeing is considered "malware," feel free to create an issue and discuss it.  That's why we do things this way. :smile:
