---
layout: post
title: Zend Framework 2.5.0 Released!
date: 2015-06-03 21:00
update: 2015-06-03 21:00
author: Matthew Weier O'Phinney
url_author: http://mwop.net/
permalink: /blog/zend-framework-2-5-0-released.html
categories:
- blog
- released

---

Today we've released Zend Framework 2.5.0!

 I'm not going to provide a link to the downloads page, as this release marks a radical change for Zend Framework 2: as of this release, all components are now developed in their own separate repositories, and Zend Framework is itself essentially only a metapackage that aggregates the components via [Composer](https://getcomposer.org)!

 The impact on users is transparent; a `composer update` will pick up the new version, which will in turn install the individual components.

### Impact

There are a few potential issues for users upgrading to 2.5.0.

 First, for those users who were incorporating the repository via git submodules, that approach will no longer work, as the ZF2 repository no longer contains code! If you are doing this, you will either need to start using Composer, or add every component as a git submodule, which will likely also require setting up custom autoloading.

 Second, for users who were using the download packages we previously had available via our [Downloads page](/downloads/latest), we are not currently providing a package. You can safely stay at version 2.4 (which is our [long-term support](/long-term-support) version) for now. We are evaluating re-instating full download packages in the future, but need to gauge interest and how much effort will be needed to automate such packaging.

 Third, for users of our translation resources, the translation files are no longer in the `resources/languages/` directory. This is because they now have their own dedicated package, [zendframework/zend-i18n-resources](https://github.com/zendframework/zend-i18n-resources)! As such, you cannot just point your code at that directory in your ZF2 install; you will need to do a little bit of work to integrate. The repository has full information on how you can accomplish that.

 Finally, we have a significant bump in our minimum supported PHP version starting with 2.5.0: we now require PHP 5.5+. PHP 5.3 is no longer receiving even security updates at this time, and [PHP 5.4 support ends on 14 September 2015](http://php.net/supported-versions.php) — just over 3 months from now. We encourage our users on versions prior to 5.5 to migrate immediately; the migration from 5.4 to 5.5 or 5.6 is trivial, and you'll get substantial performance benefits in addition to new features.

### Changes

 Other than the major architectural change and the PHP version bump, the code in 2.5.0 is exactly the same as you have in 2.4.2.

### Components

 The following is a listing of the various components that make up Zend Framework, linked to their GitHub repository. Each component contains full history of changes for that component since the 2.0.0 release.

- [Zend\\Authentication (zend-authentication)](https://github.com/zendframework/zend-authentication)
- [Zend\\Barcode (zend-barcode)](https://github.com/zendframework/zend-barcode)
- [Zend\\Cache (zend-cache)](https://github.com/zendframework/zend-cache)
- [Zend\\Captcha (zend-captcha)](https://github.com/zendframework/zend-captcha)
- [Zend\\Code (zend-code)](https://github.com/zendframework/zend-code)
- [Zend\\Config (zend-config)](https://github.com/zendframework/zend-config)
- [Zend\\Console (zend-console)](https://github.com/zendframework/zend-console)
- [Zend\\Crypt (zend-crypt)](https://github.com/zendframework/zend-crypt)
- [Zend\\Db (zend-db)](https://github.com/zendframework/zend-db)
- [Zend\\Debug (zend-debug)](https://github.com/zendframework/zend-debug)
- [Zend\\Di (zend-di)](https://github.com/zendframework/zend-di)
- [Zend\\Dom (zend-dom)](https://github.com/zendframework/zend-dom)
- [Zend\\Escaper (zend-escaper)](https://github.com/zendframework/zend-escaper)
- [Zend\\EventManager (zend-eventmanager)](https://github.com/zendframework/zend-eventmanager)
- [Zend\\Feed (zend-feed)](https://github.com/zendframework/zend-feed)
- [Zend\\File (zend-file)](https://github.com/zendframework/zend-file)
- [Zend\\Filter (zend-filter)](https://github.com/zendframework/zend-filter)
- [Zend\\Form (zend-form)](https://github.com/zendframework/zend-form)
- [Zend\\Http (zend-http)](https://github.com/zendframework/zend-http)
- [Zend\\I18n (zend-i18n)](https://github.com/zendframework/zend-i18n)
- [Zend\\InputFilter (zend-inputfilter)](https://github.com/zendframework/zend-inputfilter)
- [Zend\\Json (zend-json)](https://github.com/zendframework/zend-json)
- [Zend\\Ldap (zend-ldap)](https://github.com/zendframework/zend-ldap)
- [Zend\\Loader (zend-loader)](https://github.com/zendframework/zend-loader)
- [Zend\\Log (zend-log)](https://github.com/zendframework/zend-log)
- [Zend\\Mail (zend-mail)](https://github.com/zendframework/zend-mail)
- [Zend\\Math (zend-math)](https://github.com/zendframework/zend-math)
- [Zend\\Memory (zend-memory)](https://github.com/zendframework/zend-memory)
- [Zend\\Mime (zend-mime)](https://github.com/zendframework/zend-mime)
- [Zend\\ModuleManager (zend-modulemanager)](https://github.com/zendframework/zend-modulemanager)
- [Zend\\Mvc (zend-mvc)](https://github.com/zendframework/zend-mvc)
- [Zend\\Navigation (zend-navigation)](https://github.com/zendframework/zend-navigation)
- [Zend\\Paginator (zend-paginator)](https://github.com/zendframework/zend-paginator)
- [Zend\\Permissions\\Acl (zend-permissions-acl)](https://github.com/zendframework/zend-permissions-acl)
- [Zend\\Permissions\\Rbac (zend-permissions-rbac)](https://github.com/zendframework/zend-permissions-rbac)
- [Zend\\ProgressBar (zend-progressbar)](https://github.com/zendframework/zend-progressbar)
- [Zend\\Serializer (zend-serializer)](https://github.com/zendframework/zend-serializer)
- [Zend\\Server (zend-server)](https://github.com/zendframework/zend-server)
- [Zend\\ServiceManager (zend-servicemanager)](https://github.com/zendframework/zend-servicemanager)
- [Zend\\Session (zend-session)](https://github.com/zendframework/zend-session)
- [Zend\\Soap (zend-soap)](https://github.com/zendframework/zend-soap)
- [Zend\\Stdlib (zend-stdlib)](https://github.com/zendframework/zend-stdlib)
- [Zend\\Tag (zend-tag)](https://github.com/zendframework/zend-tag)
- [Zend\\Test (zend-test)](https://github.com/zendframework/zend-test)
- [Zend\\Text (zend-text)](https://github.com/zendframework/zend-text)
- [Zend\\Uri (zend-uri)](https://github.com/zendframework/zend-uri)
- [Zend\\Validator (zend-validator)](https://github.com/zendframework/zend-validator)
- [Zend\\Version (zend-version)](https://github.com/zendframework/zend-version)
- [Zend\\View (zend-view)](https://github.com/zendframework/zend-view)
- [Zend\\XmlRpc (zend-xmlrpc)](https://github.com/zendframework/zend-xmlrpc)
- [ZendXml](https://github.com/zendframework/ZendXml)

### New Components

We also have two new components in the Zend Framework family:

- [Diactoros](https://github.com/zendframework/zend-diactoros), a [PSR-7](http://www.php-fig.org/psr/psr-7) implementation, providing HTTP message, URI, uploaded file, and stream implementations.
- [Stratigility](https://github.com/zendframework/zend-stratigility), a PSR-7-compatible middleware implementation based on [Sencha Connect](https://github.com/senchalabs/connect).

 These are in their early 1.0 versions, though fully stable. We'll be discussing them in more detail in later blog posts. If you want information now, Matthew recently delivered a [webinar on PSR-7 and Stratigility](http://info.zend.com/Lq80CX0040Ue0LMxR0A0j0r).

### The Future!

 This release marks the completion of the first major milestone towards Zend Framework 3! With the various components now versioned on their own timelines and in their own repositories, we can start cherry-picking which components need refactoring or new features. Along the way, we will be creating teams of interested contributors to maintain specific components, which should help accelerate development velocity.

 In the near future, we will be working on introducing PSR-7 and middleware support in the ZF2 MVC layer, as well as creating a workflow for wrapping the ZF2 MVC inside of PSR-7-based middleware to allow execution alongside other frameworks and code bases.

### Thank Yous

 Splitting the components into their own repositories and setting up the metapackage approach for the ZF2 repository was not easy. Fortunately, we had some very motivated contributors to assist along the way. In particular:

- [Gianluca Arebezzano](http://gianarb.it/) and [Corley](http://www.corley.it/) (an Italian AWS partner). Gianluca suggested we perform the component splits in parallel via AWS, and convinced Corley, where he works, to help make it happen. Because of this generous support, we were able to do what would have taken weeks in a matter of a single day.
- [Maks3w](https://github.com/maks3w), one of our community review team, who did a ton of work around our testing and continuous integration structure to ensure that the rewritten component repositories could be tested seamlessly.

 Version 2.5.0 is only the beginning; you'll be seeing some exciting changes in the Zend Framework project soon!