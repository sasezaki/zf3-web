---
layout: post
title: Zend Framework 2.1.5 Released!
date: 2013-04-17 20:00
update: 2013-04-17 20:00
author: Matthew Weier O'Phinney
url_author: http://mwop.net/
permalink: /blog/zend-framework-2-1-5-released.html
categories:
- blog
- released

---

 The Zend Framework community is pleased to announce the immediate availability of Zend Framework 2.1.5! Packages and installation instructions are available at:

- [http://framework.zend.com/downloads/latest](/downloads/latest)

 This is a monthly maintenance release.

Notable changes
---------------

 2.1.5 is a monthly maintenance release, and the bulk of issues resolved were primarily centered around code maintainability - docblocks typos were corrected, internal variables renamed more semantically, etc. However, a few changes are notable:

- A long-standing issue [regarding setting global permissions in `Zend\Permissions\Acl`](https://github.com/zendframework/zf2/pull/4226) was resolved.
- [`Zend\Db\Metadata` was updated to no longer use the untrusted `quoteValue()` API](https://github.com/zendframework/zf2/pull/4241); this means it will no longer create notices!
- [Filter priority settings are no longer lost when merging filter chains.](https://github.com/zendframework/zf2/pull/4148)
- [The stop-propagation flag is now reset when triggering an event.](https://github.com/zendframework/zf2/pull/4147) This solves a problem that occurred in the MVC when triggering multiple different events in succession.
- A fix was applied to prevent [`Zend\Console` from bleeding color to the next line](https://github.com/zendframework/zf2/pull/4168).
- `Zend\Navigation` now [supports query parameters properly](https://github.com/zendframework/zf2/pull/4084).
- [Forms now allow empty collections](https://github.com/zendframework/zf2/issues/3373)
- [`Zend\Navigation` now properly injects pages with dependencies](https://github.com/zendframework/zf2/issues/2898).

Manual improvements
-------------------

 Last month, we held our first [documentation hunt](http://framework.zend.com/blog//2013-03-28-help-us-improve-the-documentation.html), resulting in a lot of documentation improvements.

 Additionally, we began an effort to provide Zend Framework 1 -> Zend Framework 2 migration information. [A preview is available on readthedocs.org](http://zf2.readthedocs.org/en/latest/migration/overview.html).

Changelog
---------

 Almost 100 patches were applied to the ZF2 codebase, and dozens to the documentation. The full changelog for 2.1.5 is available:

- [http://framework.zend.com/changelog/2.1.5](/changelog/2.1.5)

Thank You!
----------

 I'd like to thank everyone who provided issue reports, typo fixes, maintenance improvements, bugfixes, and documentation improvements; your efforts make the framework increasingly better!

Roadmap
-------

 Maintenance releases happen monthly on the third Wednesday. Version 2.2.0 will release in the first half of May, with the first release candidate dropping during the week of 29 April - 3 May 2013.