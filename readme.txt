﻿=== Simple History ===
Contributors: eskapism
Donate link: http://eskapism.se/sida/donate/
Tags: history, log, changes, changelog, audit, trail, pages, attachments, users, cms, dashboard, admin, syslog, feed, activity, stream
Requires at least: 3.6.0
Tested up to: 4.2.2
Stable tag: 2.1.1

View changes made by users within WordPress. See who created a page, uploaded an attachment or approved an comment, and more.

== Description ==

Simple History shows recent changes made within WordPress, directly on your dashboard or on a separate page.

The plugin works as a log/history/audit log/version history of the most important events that occur in WordPress.

Out of the box Simple History has support for:

* **Posts and pages**<br>
see who added, updated or deleted a post or page
* **Attachments**<br>
see who added, updated or deleted an attachment
* **Comments**<br>
see who edited, approved or removed a comment
* **Widgets**<br>
get info when someone adds, updates or removes a widget in a sidebar
* **Plugins**<br>
activation and deactivation
* **User profiles**<br>
info about added, updated or removed users
* **User logins**<br>
see when a user login & logout
* **Failed user logins**<br>
see when someone has tried to log in, but failed. The log will then include ip address of the possible hacker.

There is also a **RSS feed of changes** available, so you can keep track of the changes made via your favorite RSS reader on your phone, on your iPad, or on your computer.

It’s a plugin that is good to have on websites where several people are
involved in editing the content.

The plugin works fine on [multisite installations of WordPress](http://codex.wordpress.org/Glossary#Multisite) too.

#### Example scenarios

Keep track of what other people are doing:
_"Has someone done anything today? Ah, Sarah uploaded
the new press release and created an article for it. Great! Now I don't have to do that."_

Or for debug purposes:
_"The site feels slow since yesterday. Has anyone done anything special? ... Ah, Steven activated 'naughy-plugin-x',
that must be it."_

#### See it in action

See the plugin in action with this short screencast:
[youtube http://www.youtube.com/watch?v=4cu4kooJBzs]

#### API so you can add your own events to Simple History

If you are a theme or plugin developer and would like to add your own things/events to Simple History you can do that by calling the function `simple_history_add()` like this:

`
<?php

if ( function_exists("SimpleLogger") ) {

    // Most basic example: just add some information to the log
    SimpleLogger()->info("This is a message sent to the log");

    // A bit more advanced: log events with different severities
    SimpleLogger()->info("User admin edited page 'About our company'");
    SimpleLogger()->warning("User 'Jessie' deleted user 'Kim'");
    SimpleLogger()->debug("Ok, cron job is running!");

}
?>
`

#### Translations/Languages

So far Simple History is translated to:

* Swedish
* German
* Polish
* Danish
* Dutch
* Finnish

I'm looking for translations of Simple History in more languages! If you're interested please check out the [localization](https://developer.wordpress.org/plugins/internationalization/localization/) part of the Plugin Handbook for info on how to translate plugins. When you're done with your translation email it to me at par.thernstrom@gmail.com, or [add a pull request](https://github.com/bonny/WordPress-Simple-History/).

#### Contribute at GitHub

Development of this plugin takes place at GitHub. Please join in with feature requests, bug reports, or even pull requests!
https://github.com/bonny/WordPress-Simple-History

#### Donation & more plugins

* If you like this plugin don't forget to [donate to support further development](http://eskapism.se/sida/donate/).
* More [WordPress CMS plugins](http://wordpress.org/extend/plugins/profile/eskapism) by the same author.


== Screenshots ==

1. The log view + it also shows the filter function in use - the log only shows event that
are of type post and pages and media (i.e. images & other uploads), and only events
initiated by a specific user.

2. Events with different severity – Simple History uses the log levels specified in the PHP PSR-3 standard.

3. Events have context with extra details - Each logged event can include useful rich formatted extra information. For example: a plugin install can contain author info and a the url to the plugin, and an uploaded image can contain a thumbnail of the image.

4. Click on the IP address of an entry to view the location of for example a failed login attempt.


== Changelog ==

## Changelog

= trunk (June 2015) =

- Changed: By default the log now shows events from the last week. The previous behavior was to not apply any filtering what so ever during the first load. Anyway – this change makes it possible to load the log very quickly even for very large logs. A large amount of users + keeping the log forver = millions of rows of data. Previosly this could stall the log or make it load almost forever. Now = almost always very fast. Tried it with over 5.000 users and a million row and yes - zing! - much faster..
- Added: Finnish translation. Thanks a lot to the translator!
- Added: Cache is used on a few more places.
- Fixed: The function that checks for new rows each second (or actually each tenth second to spare resourced) was called an extra time each time the submit button for the filter was clicked. Kinda stupid. Kinda fixed now.
- Fixed: The export feature that was added in version 2.1 was actually not enabled for all users. Now it is!

= 2.1.1 (May 2015) =

- Removed: filter `simple_history/dropins_dir` removed. 
- Changed: Dropins are not loaded from a `glob()` call anymore (just like plugins in the prev release)
- Updated: Brazilian Portuguese translation updated.
- Fixed: POT file updated for translators.
- Fixed: Better sanitization of API arguments.


= 2.1 (May 2015) =

- Added: Export! Now it's possible to export the events log to a JSON or CSV formatted file. It's your data so you should be able to export it any time you want or need. And now you can do that. You will find the export function in the Simple History settings page (Settings -> Simple History).
- Added: Filter `simple_history/add_custom_logger` and function `register_logger` that together are used to load external custom loggers. See [example-logger.php](https://github.com/bonny/WordPress-Simple-History/blob/master/examples/example-logger.php) for usage example.
- Added: Filter `simple_history/header_initiator_use_you`.
- Fixed: Fixed an undefined variable in get_avatar(). Fixes https://github.com/bonny/WordPress-Simple-History/issues/74.
- Fixed: When using [HyperDB](https://wordpress.org/support/plugin/hyperdb) only one event was returned. Fixed by using [adding `NO_SELECT_FOUND_ROWS` to the query](https://plugins.trac.wordpress.org/browser/hyperdb/trunk/db.php?#L49). Should fix problems for users using HyperDB and also users using for example [wpengine.com](http://wpengine.com) (that probably also is using HyperDB or a similar approach).
- Changed: Loggers now get default capability "manage_options" if they have no capability set.
- Changed: Misc internal cleanup.
- Removed: filter `simple_history/loggers_dir` removed, because loggers are loaded from array instead of file listing generated from `glob()`. Should be (however to the eye non-noticable) faster.

= 2.0.30 (May 2015) =

- Added: Username of logged events now link to that user's profile.
- Fixed: When expanding ocassions the first loaded occasion was the same event as the one you expanded from, and the last ocassion was missing. Looked extra stupid when only 1 occasion existed, and you clicked "show ocassions" only to just find the same event again. So stupid. But fixed now!
- Fixed: If an event had many similar events the list of similar events could freeze the browser. ([17948 failed login attempts overnight](https://twitter.com/eskapism/status/595478847598002176) is not that uncommon it turns out!)
- Fixed: Some loggers were missing the "All"-message in the search.
- Changed: Hide some more keys and values by default in the context data popup.
- Changed: Use `truncate` instead of `delete` when clearing the database. Works much faster on large logs.

= 2.0.29 (April 2015) =

- Added: Introducing [Post "Quick Diff"](http://eskapism.se/blog/2015/04/quick-diff-shows-post-changes-in-wordpress/) – a very simple and efficient way to quickly see what’s been changed in a post. With Quick Diff you will in a glance see the difference between the title, permalink, content, publish date, post status, post author, or the template of the post. It's really a super simple and fast way to follow the work of your co-editors.
- Added: Filter to add custom HTML above and after the context data table. They are named `simple_history/log_html_output_details_single/html_before_context_table` and `simple_history/log_html_output_details_single/html_after_context_table` (and yes, I do fancy really long filter names).
- Added: Filters to control what to output in the data/context details table (the popup you see when you click the time of each event): `simple_history/log_html_output_details_table/row_keys_to_show` and `simple_history/log_html_output_details_table/context_keys_to_show`. Also added [two usage examples](https://github.com/bonny/WordPress-Simple-History/blob/master/examples/examples.php) for the filters.
- Added: Filter `simple_history/log_insert_context` to control what gets saved to the context table. Example on usage for this is also available in the [example file](https://github.com/bonny/WordPress-Simple-History/blob/master/examples/examples.php).
- Added: data attribute `data-ip-address-multiple` and class `SimpleHistoryLogitem--IPAddress-multiple` added for events that have more than one IP address detected. Happens when `http_x_forwarded_for` or similar headers are included in response.
- Updated: Danish translation updated.
- Fixed: Images in GitHub readme files are now displayed correctly.
- Fixed: Readme files to GitHub repositories ending with slash (/) now works correctly too.
- Fixed: IP Info popup is now again closeable with `ESC` key or with a click outside it.
- Fixed: Some enqueued scripts had double slashes in them.
- Fixed: Make sure [URLs from add_query_arg() gets escaped](https://make.wordpress.org/plugins/2015/04/20/fixing-add_query_arg-and-remove_query_arg-usage/).
- Fixed: Some other small things.

= 2.0.28 (April 2015) =

- Fixed: Do not try to load the Translation Install API if using WordPress before 4.0. Fixes https://github.com/bonny/WordPress-Simple-History/issues/67.
- Updated: German translation updated.

= 2.0.27 (April 2015) =

- Fixed: Even better support for plugins from GitHub with the `GitHub Plugin URI` header. Plugin install, deactivations, and activations should have correct view-info-links now.
- Updated: German translation updated.
- Updated: Swedish translation updated.

= 2.0.26 (March 2015) =

- Fixed: Plugin installs from wordpress.org would show "wordpress plugin directory" as their source file. Looked stupid. Fixed now!
- Added: `composer.json` added, so Simple History can be pulled in to other projects via [Composer](https://getcomposer.org/). Actually untested, but at least the file is there. Please let me know if it works! :)

= 2.0.25 (March 2015) =

- Added: Plugin installs now shows the source of the plugin. Supported sources are "WordPress plugin repository" and "uploaded ZIP archives".
- Added: Plugin installs via upload now shows the uploaded file name.
- Added: Support for showing plugin info-link for plugins from GitHub, installed with uploaded ZIP-archive. Only tested with a few plugins. Please let me know if it works or not!
- Fixed: Messages for disabled loggers was not shown.
- Fixed: An error when trying to show edit link for deleted comments.
- Fixed: Use a safer way to get editable roles. Hopefully fixes https://wordpress.org/support/topic/php-warnings-simpleloggerphp-on-line-162.
- Fixed: Some notice warnings from the comments logger.
- Changed: Some other small things too.

= 2.0.24 (March 2015) =

- Fixed: Plugin installs from uploaded ZIP files are now logged correctly. Fixes https://github.com/bonny/WordPress-Simple-History/issues/59.
- Fixed: Check that JavaScript variables it set and that the object have properties set. Fixes https://wordpress.org/support/topic/firefox-37-js-error-generated-by-simplehistoryipinfodropinjs.
- Updated: German translation updated.
- Changed: Loading of loggers, dropins, and so one are moved from action `plugins_loaded` to `after_setup_theme` so themes can actually use for example the load_dropin_*-filters...
- Changed: Misc small design fixes.

= 2.0.23 (March 2015) =

- Added: Filter `simple_history/rss_item_link`, so plugins can modify the link used in the RSS feed.
- Added: Links for changed posts and attachments in RSS feed now links directly to WordPress admin, making is easier to follow things from your RSS reeder.
- Added: Filters to hide history dashboard widget and history dashboard page. Filters are `simple_history/show_dashboard_widget` and `simple_history/show_dashboard_page`.
- Fixed: A missing argument error when deleting a plugin. Fixes https://wordpress.org/support/topic/warning-missing-argument-1-for-simplepluginlogger.

= 2.0.22 (February 2015) =

- Fixed: Deleted plugins were not logged correctly (name and other info was missing).
- Added: Filter `simple_history/logger/load_logger` and `simple_history/dropin/load_dropin` that can be used to control the loading of each logger or dropin. See [example file](https://github.com/bonny/WordPress-Simple-History/blob/master/examples/examples.php) for usage examples.
- Fixed: modal window with context data now works better on small screens.
- Changed: Misc internal changes.

= 2.0.21 (February 2015) =

- Added: Updates via XML RPC are now logged, for example when using the WordPress app for iOS or Android. Supported actions for now is post/page created, edited, deleted, and media uploads.
- Added: `_xmlrpc_request` is added to context of event when an event is initiated through a XML-RPC all.
- Changed: RSS feed now has loglevel of event prepended to the title.
- Changed: Options logger now only shows the first 250 chars of new and old option values. Really long values could make the log look strange.
- Added: If constant `SIMPLE_HISTORY_LOG_DEBUG` is defined and true automatically adds `$_GET`, `$_POST`, and more info to each logged event. Mostly useful for the developer, but maybe some of you are a bit paranoid and want it too.
- Updated: German translation updated.

= 2.0.20 (February 2015) =

- Added: changes via [WP-CLI](http://wp-cli.org) is now detected (was previously shown as "other").
- Added: severity level (info, warning, debug, etc.) of event is includes in the RSS output.
- Changed the way user login is logged. Should fix https://github.com/bonny/WordPress-Simple-History/issues/40 + possible more related issues.
- Added: filter `simple_history/simple_logger/log_message_key` added, that can be used to shortcut log messages. See [example file](https://github.com/bonny/WordPress-Simple-History/blob/master/examples/examples.php) for usage. Fixes https://wordpress.org/support/topic/stop-logging-certain-types-of-activity.
- Added: now uses object caching at some places. Should speed up some parts of the plugin for users with caching enabled.
- Fixed: IP info popup can now be closed with `esc`.
- Fixed: works better on small screens (like mobile phones) + misc other style related fixes.

= 2.0.19 (February 2015) =

- Added: Dutch translation by [https://github.com/niknetniko](https://github.com/niknetniko). Thanks!
- Changed: better compatibilty with plugins like [WP User Avatar](https://wordpress.org/plugins/wp-user-avatar/).
- Updated: German translation update.

= 2.0.18 (January 2015) =

- Fixed: really correctly show the version number of the previous version!

= 2.0.17 (January 2015) =

- Added: messages added using for example `SimpleLogger()->info( __("My log message") )` that have translations now auto translated the message back to english before storing the message (together with the text domain). Then upon retrieval it uses the english message + the text domain to translate the message to the currently selected language. This makes it easier to make multilingual log entries. (Yeah, I know its hard to understand what the heck this does, but it's something good and cool, trust me!)
- Added: A sidebar with text contents on the history page.
- Changed: Search now shows only the search box by default, with a link to show all search options.
- Fixed: Search is now available at the dashboard again. Hooray!
- Fixed: Old entries were not cleared automatically. Now it correctly removes old events, so your database will not risk growing to large.
- Fixed: Quick stats could show two messages sometimes.
- Fixed: When headers like `HTTP_X_FORWARDED_FOR` exists all valid IPs in that header is now stored.
- Fixed: Plugin updates via third party software like [InfiniteWP](http://infinitewp.com/) should now correctly show the version number of the previous version.
- Updated: German translation updated.
- Notice: Do you read these messages? Then you must love this plugin! Come on then, [go and give it a nice review](https://wordpress.org/support/view/plugin-reviews/simple-history).

= 2.0.16 (January 2015) =

- Fixed: Use the [X-Forwarded-For header](http://en.wikipedia.org/wiki/X-Forwarded-For), if it is set, to determine remote IP address. Should now correctly store IP addresses for servers behind load balancers or for clients going through proxies. Fixes https://wordpress.org/support/topic/use-x-forwarded-for-http-header-when-logging-remote_addr.
- Changed: Failed login attempts from unknown and known users are now grouped together. This change was made because a hacker could make many login attempts to a site and rotate the logins, so they would try with both existing and non existing user names, which would make the log flood with failed login attempts.
- Changed: use "n similar events" instead of "n more", to more cleary mark that the grouped events are not necessary exactly the same kind.
- Changed: Quick stats text changed, to also include other sources. Previous behavior was to only include events from WordPress users, but now also events from anonymous users and WordPress (like from WP-Cron) are included.

= 2.0.15 (January 2015) =

- Fixed: Widget changes where not always translated.
- Fixed: More RSS fixes to make feed valid. Maybe even for real this time.
- Updated: German translation updated.

= 2.0.14 (January 2015) =

- Added: Danish translation added. Thanks [ThomasDK81](https://github.com/ThomasDK81)!
- Misc translation fixes, for example the log levels where not translateable (it may be a good idea to keep the original English ones however because they are the ones that are common in other software).

= 2.0.13 (January 2015) =

- Fixed: RSS feed is now valid according to http://validator.w3.org/. Fixes https://wordpress.org/support/topic/a-feed-which-was-valid-under-v206-is-no-longer-under-v209-latest.
- Translation fixes. Thanks [ThomasDK81](https://github.com/ThomasDK81)!

= 2.0.12 (January 2015) =

- Fixed: Deleted attachments did not get translations.
- Fixed: A notice when showing details for a deleted attachment.

= 2.0.11 (January 2015) =

- Fixed: Comments where not logged correctly.
- Fixed: Comments where not translated correctly.
- Updated: German translation updated.

= 2.0.10 (January 2015) =

- Updated: Polish translation updated. Thanks [https://github.com/m-czardybon](m-czardybon)!
- Updated: German translation updated. Thanks [http://klein-aber-fein.de/](Ralph)!
- Updated: Swedish translation updated.

= 2.0.9 (December 2014) =

- Actually enable IP address lookup for all users. Sorry for missing to do that! ;)

= 2.0.8 (December 2014) =

- Added: IP addresses can now be clicked to view IP address info from [ipinfo.io](http://ipinfo.io). This will get you the location and network of an IP address and help you determine from where for example a failed login attempt originates from. [See screenshot of IP address info in action](http://glui.me/?d=y89nbgmvmfnxl4r/ip%20address%20information%20popup.png/).
- Added: new action `simple_history/admin_footer`, to output HTML and JavaScript in footer on pages that belong to Simple History
- Added: new trigger for JavaScript: `SimpleHistory:logReloadStart`. Fired when the log starts to reload, like when using the pagination or using the filter function.
- Fixed: use Mustache-inspired template tags instead of Underscore default ones, because they don't work with PHP with asp_tags on.
- Updated: Swedish translation updated

= 2.0.7 (December 2014) =

- Fix: no message when restoring page from trash
- Fix: use correct width for media attachment
- Add: filter `simple_history/logrowhtmloutput/classes`, to modify HTML classes added to each log row item

= 2.0.6 (November 2014) =

- Added: [WordPress 4.1 added the feature to log out a user from all their sessions](http://codex.wordpress.org/Version_4.1#Users). Simple History now logs when a user is logged out from all their sessions except the current browser, or if an admin destroys all sessions for a user. [View screenshot of new session logout log item](https://dl.dropboxusercontent.com/s/k4cmfmncekmfiib/2014-12-simple-history-changelog-user-sessions.png)

- Added: filter to shortcut loading of a dropin. Example that completely skips loading the RSS-feed-dropin:
`add_filter("simple_history/dropin/load_dropin_SimpleHistoryRSSDropin", "__return_false");`

= 2.0.5 (November 2014) =

- Fix undefined variable in plugin logger. Fixes https://wordpress.org/support/topic/simple-history-201-is-not-working?replies=8#post-6343684.
- Made the dashboard smaller
- Misc other small GUI changes

= 2.0.4 (November 2014) =

- Make messages for manually updated plugins and bulk updated plugins more similar

= 2.0.3 (November 2014) =

- Show the version of PHP that the user is running, when the PHP requirement of >= 5.3 is not met

= 2.0.2 (November 2014) =

- Fixed wrong number of arguments used in filter in RSS-feed

= 2.0.1 (November 2014) =

- Removed anonymous function in index file causing errors during install on older versions of PHP

= 2.0 (November 2014) =

Major update - Simple History is now better and nicer than ever before! :)
I've spend hundreds of hours making this update, so if you use it and like it please [donate to keep my spirit up](http://eskapism.se/sida/donate/) or [give it a nice review](https://wordpress.org/support/view/plugin-reviews/simple-history).

- Code cleanup and modularization
- Support for log contexts
- Kinda PSR-3-compatible :)
- Can handle larger logs (doesn't load whole log into memory any more)
- Use nonces at more places
- More filters and hooks to make it easier to customize
- Better looking! well, at least I think so ;)
- Much better logging system to make it much easier to create new loggers and to translate logs into different languages
- Features as plugins: more things are moved into modules/its own file
- Users see different logs depending on their capability, for example an administrator will see what plugins have been installed, but an editor will not see any plugin related logs
- Much much more.

= 1.3.11 =
- Don't use deprecated function get_commentdata(). Fixes https://wordpress.org/support/topic/get_commentdata-function-is-deprecated.
- Don't use mysql_query() directly. Fixes https://wordpress.org/support/topic/deprecated-mysql-warning.
- Beta testers wanted! I'm working on the next version of Simple History and now I need some beta testers. If you want to try out the shiny new and cool version please download the [v2 branch](https://github.com/bonny/WordPress-Simple-History/tree/v2) over at GitHub. Thanks!

= 1.3.10 =
- Fix: correct usage of "its"
- Fix: removed serif font in log. Fixes https://wordpress.org/support/topic/two-irritations-and-pleas-for-change.

= 1.3.9 =
- Fixed strict standards warning
- Tested on WordPress 4.0

= 1.3.8 =
- Added filter for rss feed: `simple_history/rss_feed_show`. Fixes more things in this thread: http://wordpress.org/support/topic/more-rss-feed-items.

= 1.3.7 =
- Added filter for rss feed: `simple_history/rss_feed_args`. Fixes http://wordpress.org/support/topic/more-rss-feed-items.

= 1.3.6 =
- Added Polish translation
- Added correct XML encoding and header
- Fixed notice warnings when media did not exist on file system

= 1.3.5 =
- Added a reload-button at top. Click it to reload the history. No need to refresh page no more!
- Fixed items being reloaded when just clicking the dropdown (not having selected anything yet)
- Fixed bug with keyboard navigation
- Added Portuguese translation by [X6Web](http://x6web.com)
- Use less SQL queries

= 1.3.4 =
- Changed the way post types show in the dropdown. Now uses plural names + not prefixed with main post type. Looks better I think. Thank to Hassan for the suggestion!
- Added "bytes" to size units that an attachment can have. Also fixes undefined notice warning when attachment had a size less that 1 KB.

= 1.3.3 =
- Capability for viewing settings changed from edit_pages to the more correct [manage_options](http://codex.wordpress.org/Roles_and_Capabilities#manage_options)

= 1.3.2 =
- Could get php notice warning if rss secret was not set. Also: make sure both public and private secret exists.

= 1.3.1 =
- Improved contrast for details view
- Fix sql error on installation due to missing column
- Remove options and database table during removal of plugin
- Added: German translation for extender module

= 1.3 =
- Added: history events can store text description with a more detailed explanation of the history item
- Added: now logs failed login attempts for existing username. Uses the new text description to store more info, for example user agent and remote ip address (REMOTE_ADDR)
- Fixed: box did not change height when clicking on occasions
- Fixed: use on() instead of live() in JavaScript

= 1.2 =
- Fixed: Plugin name is included when plugins is activated or deactivated. Previosuly only folder name and name of php file was included.
- Added: Attachment thumbnails are now visible if history item is an attachment. Also includes some metadata.
- Changed: Filters now use dropdowns for type and user. When a site had lots of users and lots of post types, the filter section could be way to big.
- Added keyboard navigation. Use right and left arrow when you are on Simple History's own page to navigation between next and previous history page.
- Added loading indicator, so you know it's grabbing your history, even if it's taking a while
- Misc JS and CSS fixes
- Arabic translation updated
- POT-file updated

= 1.1 =
- Added the Simple History Extender-module/plugin. With this great addon to Simple History it is very easy for other developers to add their own actions to simple history, including a settings panel to check actions on/off. All work on this module was made by Laurens Offereins (lmoffereins@gmail.com). Super thanks!
- With the help of Simple History Extender this plugin also tracks changes made in bbPress, Gravity Forms and in Widges. Awesome!
- Added user email to RSS feed + some other small changed to make it compatible with IFTTT.com. Thanks to phoenixMagoo for the code changes. Fixes http://wordpress.org/support/topic/suggestions-a-couple-of-tweaks-to-the-rss-feed.
- Added two filters for the RSS feed: simple_history_rss_item_title and simple_history_rss_item_description.
- Changed the way the plugin directory was determined. Perhaps and hopefully this fixes some problems with multi site and plugin in different locations and stuff like that
- Style fixes for RTL languages
- Small fixes here and there, for example changing deprecated WordPress functions to not deprecated
- Added new filter: simple_history_db_purge_days_interval. Hook it to change default clear interval of 60 days.

= 1.0.9 =
- Added French translation

= 1.0.8 =
- Added: filter simple_history_allow_db_purge that is used to determine if the history should be purged/cleaned after 60 days or not. Return false and it will never be cleaned.
- Fixed: fixed a security issue with the RSS feed. User who should not be able to view the feed could get access to it. Please update to this version to keep your change log private!

= 1.0.7 =
- Fixed: Used a PHP shorthand opening tag at a place. Sorry!
- Fixed: Now loads scripts and styles over HTTPS, if that's being used. Thanks to "llch" for the patch.

= 1.0.6 =
- Added: option to set number of items to show, per page. Default i 5 history log items.

= 1.0.5 =
- Fixed: some translation issues, including updated POT-file for translators.

= 1.0.4 =
- You may want to clear the history database after this update because the items in the log will have mixed translate/untranslated status and it may look/work a bit strange.
- Added: Option to clear the database of log items.
- Changed: No longer stored translated history items in the log. This makes the history work even if/when you switch langauge of WordPress.
- Fixed: if for example a post was editied several times and during these edits it changed name, it would end up at different occasions. Now it's correctly stored as one event with several occasions.
- Some more items are translateable

= 1.0.3 =
- Updated German translation
- Some translation fixes

= 1.0.2 =
- Fixed a translation bug
- Added updated German translation

= 1.0.1 =
- The pagination no longer disappear after clickin "occasions"
- Fixed: AJAX loading of new history items didn't work.
- New filter: simple_history_view_history_capability. Default is "edit_pages". Modify this to change what cabability is required to view the history.
- Modified: styles and scripts are only added on pages that use/show Simple History
- Updated: new POT file. So translators my want to update their translations...

= 1.0 =
- Added: pagination. Gives you more information, for example the number of items, and quicker access to older history items. Also looks more like the rest of the WordPress GUI.
- Modified: search now searches type of action (added, modified, deleted, etc.).

= 0.8.1 =
- Fixed some annoying errors that slipt through testing.

= 0.8 =
- Added: now also logs when a user saves any of the built in settings page (general, writing, reading, discussion, media, privacy, and permalinks. What more things do you want to see in the history? Let me know in the [support forum](http://wordpress.org/support/plugin/simple-history).
- Added: gravatar of user performing action is always shown
- Fixed: history items that was posts/pages/custom post types now get linked again
- Fixed: search is triggered on enter (no need to press search button) + search searches object type and object subtype (before it just searched object name)
- Fixed: showing/loading of new history items was kinda broken. Hopefully fixed and working better than ever now.
- Plus: even more WordPress-ish looking!
- Also added donate-links. Tried to keep them discrete. Anyway: please [donate](http://eskapism.se/sida/donate/?utm_source=wordpress&utm_medium=changelog&utm_campaign=simplehistory) if you use this plugin regularly.

= 0.7.2 =
- Default settings should be to show on page, missed that one. Sorry!

= 0.7.1 =
- Fixed a PHP shorttag

= 0.7 =
- Do not show on dashboard by default to avoid clutter. Can be enabled in settings.
- Add link to settings from plugin list
- Settings are now available as it's own page under Settings -> Simple Fields. It was previosly on the General settings page and some people had difficulties finding it there.
- Added filters: simple_history_show_settings_page, simple_history_show_on_dashboard, simple_history_show_as_page

= 0.6 =
- Changed widget name to just "History" instead of "Simple History". Keep it simple. Previous name implied there also was an "Advanced History" somewhere.
- Made the widget look a bit WordPress-ish by borrwing some of the looks from the comments widget.
- Fix for database that didn't use UTF-8 (sorry international users!)
- Some security fixes
- Updated POT-file

= 0.5 =
- Added author to RSS
- Added german translation, thanks http://www.fuerther-freiheit.info/
- Added swedish translation, thanks http://jockegustin.se
- Better support for translation

= 0.4 =
- Added: Now you can search the history
- Added: Choose if you wan't to load/show more than just 5 rows from the history

= 0.3.11 =
- Fixed: titles are now escaped

= 0.3.10 =
- Added chinese translation
- Fixed a variable notice
- More visible ok-message after setting a new RSS secret

= 0.3.9 =
- Attachment names were urlencoded and looked wierd. Now they're not.
- Started to store plugin version number

= 0.3.8 =
- Added chinese translation
- Uses WordPress own human_time_diff() instead of own version
- Fix for time zones

= 0.3.7 =
- Directly after installation of Simple History you could view the history RSS feed without using any secret. Now a secret is automatically set during installation.

= 0.3.6 =
- Made the RSS-feature a bit easier to find: added a RSS-icon to the dashboard window - it's very discrete, you can find it at the bottom right corner. On the Simple History page it's a bit more clear, at the bottom, with text and all. Enjoy!
- Added POT-file

= 0.3.5 =
- using get_the_title instead of fetching the title directly from the post object. should make plugins like qtranslate work a bit better.
- preparing for translation by using __() and _e() functions. POT-file will be available shortly.
- Could get cryptic "simpleHistoryNoMoreItems"-text when loading a type with no items.

= 0.3.4 =
- RSS-feed is now valid, and should work at more places (could be broken because of html entities and stuff)

= 0.3.3 =
- Moved JavaScript to own file
- Added comments to the history, so now you can see who approved a comment (or unapproved, or marked as spam, or moved to trash, or restored from the trash)

= 0.3.2 =
- fixed some php notice messages + some other small things I don't remember..

= 0.3.1 =
- forgot to escape html for posts
- reduced memory usage... I think/hope...
- changes internal verbs for actions. some old history items may look a bit weird.
- added RSS feed for recent changes - keep track of changes via your favorite RSS-reader

= 0.3 =
- page is now added under dashboard (was previously under tools). just feel better.
- mouse over on date now display detailed date a bit faster
- layout fixes to make it cooler, better, faster, stronger
- multiple events of same type, performed on the same object, by the same user, are now grouped together. This way 30 edits on the same page does not end up with 30 rows in Simple History. Much better overview!
- the name of deleted items now show up, instead of "Unknown name" or similar
- added support for plugins (who activated/deactivated what plugin)
- support for third party history items. Use like this:
simple_history_add("action=repaired&object_type=starship&object_name=USS Enterprise");
this would result in somehting like this:
Starship "USS Enterprise" repaired
by admin (John Doe), just now
- capability edit_pages needed to show history. Is this an appropriate capability do you think?

= 0.2 =
* Compatible with 2.9.2

= 0.1 =
* First public version. It works!
