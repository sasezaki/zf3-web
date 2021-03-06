---
layout: post
title: Zend Framework 2.0.4 Released!
date: 2012-11-21 00:00
update: 2012-11-21 00:00
author: Matthew Weier O'Phinney
url_author: http://mwop.net/
permalink: /blog/zend-framework-2-0-4-released.html
categories:
- blog
- released

---

 The Zend Framework community is pleased to announce the immediate availability of Zend Framework 2.0.4! Packages and installation instructions are available at:

- [http://framework.zend.com/downloads/latest](/downloads/latest)

Changes
-------

 ZF2 has shipped with two "view strategies" aimed at simplifying common use cases around developing JSON and XML APIs: `Zend\View\Strategy\JsonStrategy` and `Zend\View\Strategy\FeedStrategy`. Each of these would select an appropriate renderer based on one of the following criteria:

- If the view model present was of a specific type (e.g., `JsonModel`, `FeedModel`).
- If the `Accept` header contained the appropriate media type.

 This latter condition sparked some worry that, when enabled at the application level (vs. enabled based on selected module, controller, action, or other more specific criteria), any endpoint could be forced to return JSON or Atom (based on the strategies registered), regardless of whether or not it was appropriate. This could lead to a couple bad situations:

- Data present in the view model not intended for actual display now being displayed.
- Raising of exceptions due to insuitability of certain view variables for serialization in the selected format (e.g., invalid feed data, non-JSON-serializeable objects, etc.); this could lead to resource consumption and potentially other vulnerabilities.

 Based on these concerns, we made the following changes:

- The `JsonStrategy` and `FeedStrategy` now only ever select a renderer based on the current view model type: e.g. if you want to expose something as JSON, you must return a `JsonModel`.
- Introduced a new controller plugin, `acceptableViewModelSelector()`. This helper can be used to select an appropriate view model if the `Accept` header meets criteria you specify.
 
 As an example of the latter: 
    <pre class="highlight"><span style="color: #000000">
    <span style="color: #0000BB"><?php<br></br></span><span style="color: #007700">class </span><span style="color: #0000BB">SomeController </span><span style="color: #007700">extends </span><span style="color: #0000BB">AbstractActionController<br></br></span><span style="color: #007700">{<br></br>    protected </span><span style="color: #0000BB">$acceptCriteria </span><span style="color: #007700">= array(<br></br>        </span><span style="color: #DD0000">'Zend\View\Model\JsonModel' </span><span style="color: #007700">=> array(<br></br>            </span><span style="color: #DD0000">'application/json'</span><span style="color: #007700">,<br></br>        ),<br></br>        </span><span style="color: #DD0000">'Zend\View\Model\FeedModel' </span><span style="color: #007700">=> array(<br></br>            </span><span style="color: #DD0000">'application/rss+xml'</span><span style="color: #007700">,<br></br>        ),<br></br>    );<br></br><br></br>    public function </span><span style="color: #0000BB">apiAction</span><span style="color: #007700">()<br></br>    {<br></br>        </span><span style="color: #0000BB">$viewModel </span><span style="color: #007700">= </span><span style="color: #0000BB">$this</span><span style="color: #007700">-></span><span style="color: #0000BB">acceptableViewModelSelector</span><span style="color: #007700">(</span><span style="color: #0000BB">$this</span><span style="color: #007700">-></span><span style="color: #0000BB">acceptCriteria</span><span style="color: #007700">);<br></br>        <br></br>        </span><span style="color: #FF8000">// Potentially vary execution based on model returned<br></br>        </span><span style="color: #007700">if (</span><span style="color: #0000BB">$viewModel </span><span style="color: #007700">instanceof </span><span style="color: #0000BB">JsonModel</span><span style="color: #007700">) {<br></br>            </span><span style="color: #FF8000">// ...<br></br>        </span><span style="color: #007700">}<br></br>    }<br></br>}<br></br></span>
    </span>


 The above would return a standard `Zend\View\Model\ViewModel` instance if the criteria is not met, and the specified view model types if the specific criteria is met. Rules are matched in order, with the first match "winning."

Changelog
---------

 In addition to the changes mentioned above, this release included more than 40 patches, ranging from minor docblock improvements to bugfixes. The full list is as follows:

- [2808: Add serializer better inheritance and extension](https://github.com/zendframework/zf2/issues/2808)
- [2813: Add test on canonical name with the ServiceManager](https://github.com/zendframework/zf2/issues/2813)
- [2832: bugfix: The helper DateFormat does not cache correctly when a pattern is set.](https://github.com/zendframework/zf2/issues/2832)
- [2837: Add empty option before empty check](https://github.com/zendframework/zf2/issues/2837)
- [2843: change self:: with static:: in call-ing static property/method](https://github.com/zendframework/zf2/issues/2843)
- [2857: Unnecessary path assembly on return in Zend\\Mvc\\Router\\Http\\TreeRouteStack->assemble() line 236](https://github.com/zendframework/zf2/issues/2857)
- [2867: Enable view sub-directories when using ModuleRouteListener](https://github.com/zendframework/zf2/issues/2867)
- [2872: Resolve naming conflicts in foreach statements](https://github.com/zendframework/zf2/issues/2872)
- [2878: Fix : change self:: with static:: in call-ing static property/method() in other components ( all )](https://github.com/zendframework/zf2/issues/2878)
- [2879: remove unused const in Zend\\Barcode\\Barcode.php](https://github.com/zendframework/zf2/issues/2879)
- [2896: Constraints in Zend\\Db\\Metadata\\Source\\AbstractSource::getTable not initalised](https://github.com/zendframework/zf2/issues/2896)
- [2907: Fixed proxy adapter keys being incorrectly set due Zend\\Http\\Client](https://github.com/zendframework/zf2/issues/2907)
- [2909: Change format of Form element DateTime and DateTimeLocal](https://github.com/zendframework/zf2/issues/2909)
- [2921: Added Chinese translations for zf2 validate/captcha resources](https://github.com/zendframework/zf2/issues/2921)
- [2924: small speed-up of Zend\\EventManager\\EventManager::triggerListeners()](https://github.com/zendframework/zf2/issues/2924)
- [2929: SetCookie::getFieldValue() always uses urlencode() for cookie values, even in case they are already encoded](https://github.com/zendframework/zf2/issues/2929)
- [2930: Add minor test coverage to MvcEvent](https://github.com/zendframework/zf2/issues/2930)
- [2932: Sessions: SessionConfig does not allow setting non-directory save path](https://github.com/zendframework/zf2/issues/2932)
- [2937: preserve matched route name within route match instance while forwarding...](https://github.com/zendframework/zf2/issues/2937)
- [2940: change 'Cloud\\Decorator\\Tag' to 'Cloud\\Decorator\\AbstractTag'](https://github.com/zendframework/zf2/issues/2940)
- [2941: Logical operator fix : 'or' change to '||' and 'and' change to '&&'](https://github.com/zendframework/zf2/issues/2941)
- [2952: Various Zend\\Mvc\\Router\\Http routers turn + into a space in path segments](https://github.com/zendframework/zf2/issues/2952)
- [2957: Make Partial proxy to view render function](https://github.com/zendframework/zf2/issues/2957)
- [2971: Zend\\Http\\Cookie undefined self::CONTEXT\_REQUEST](https://github.com/zendframework/zf2/issues/2971)
- [2976: Fix for #2541](https://github.com/zendframework/zf2/issues/2976)
- [2981: Controller action HttpResponse is not used by SendResponseListener](https://github.com/zendframework/zf2/issues/2981)
- [2983: replaced all calls to $this->xpath with $this->getXpath() to always have...](https://github.com/zendframework/zf2/issues/2983)
- [2986: Add class to file missing a class (fixes #2789)](https://github.com/zendframework/zf2/issues/2986)
- [2987: fixed Zend\\Session\\Container::exchangeArray](https://github.com/zendframework/zf2/issues/2987)
- [2994: Fixes #2993 - Add missing asterisk to method docblock](https://github.com/zendframework/zf2/issues/2994)
- [2997: Fixing abstract factory instantiation time](https://github.com/zendframework/zf2/issues/2997)
- [2999: Fix for GitHub issue 2579](https://github.com/zendframework/zf2/issues/2999)
- [3002: update master's resources/ja Zend\_Validate.php message](https://github.com/zendframework/zf2/issues/3002)
- [3003: Adding tests for zendframework/zf2#2593](https://github.com/zendframework/zf2/issues/3003)
- [3006: Hotfix for #2497](https://github.com/zendframework/zf2/issues/3006)
- [3007: Fix for issue 3001 Zend\\Db\\Sql\\Predicate\\Between fails with min and max ...](https://github.com/zendframework/zf2/issues/3007)
- [3008: Hotfix for #2482](https://github.com/zendframework/zf2/issues/3008)
- [3009: Hotfix for #2451](https://github.com/zendframework/zf2/issues/3009)
- [3013: Solved Issue 2857](https://github.com/zendframework/zf2/issues/3013)
- [3025: Removing the separator between the hidden and the visible inputs. As the...](https://github.com/zendframework/zf2/issues/3025)
- [3027: Reduced #calls of plugin() in PhpRenderer using a cache mechanism](https://github.com/zendframework/zf2/issues/3027)
- [3029: Fixed the pre-commit script, missed the fix command](https://github.com/zendframework/zf2/issues/3029)
- [3030: Mark module as loaded before trigginer EVENT\_LOAD\_MODULE](https://github.com/zendframework/zf2/issues/3030)
- [3031: Zend\\Db\\Sql Fix for Insert's Merge and Set capabilities with simlar keys](https://github.com/zendframework/zf2/issues/3031)

Thank You!
----------

 Many thanks to all contributors to this release!

Reminder
--------

 Maintenance releases happen monthly on the third Wednesday. Additionally, we have the next minor release, 2.1.0, slated for sometime next month.