# Changelog

## [4.3.1]

- fix an issue that prevents new feeds from being added when mysql/mariadb is used as the database and the database
  timezone is not UTC (#1239)
- videos in enclosures can no longer have a width larger than the page (#1240)

## [4.3.0]

- h2 (the embedded database) has been upgraded to 2.2.224
    - this version uses a different file format than 2.1.x, the first time you start CommaFeed with this version, the
      database will be automatically converted to the new format
- add a setting to completely disable scrolling to selected entry (#1157)
- add a css class reflecting the current view mode to ease custom css rules (#1232)
- fix an issue that prevents new feeds from being added when mysql/mariadb is used as the database (#1239)

## [4.2.1]

- fix an issue that caused the tree to show an incorrect unread count after a websocket notification because entries
  that were already marked as read by a filtering expression were not ignored (#1191)

## [4.2.0]

- add a setting to display the action buttons in the footer instead of in the header on mobile (#1121)
- the websocket notification now contains everything needed to update the UI, the client no longer needs to make an API
  call to get the latest data when receiving the notification
- add a workaround to the Fever API for the Unread iOS app (#1188)
- fix an issue that caused dates to be saved incorrectly if the database server and the application server were in
  different timezones (#1187)

## [4.1.0]

- it is now possible to open the sidebar on mobile by swiping to the right (#1098)
- swiping to mark entries as read/unread changed from swiping right to left because swiping right now opens the sidebar
- the full hierarchy of categories are now displayed in the category dropdown (#1045)
- added a setting `maxEntriesAgeDays` to delete old entries based on their age during database cleanup.
  The setting is disabled by default for existing installations, except for the docker image where it is enabled and set
  to 365 days
- if user registrations are disabled on your instance which is the default behavior, users are redirected on the login
  page instead of the welcome page when not logged in (#1185)
- the sidebar resizer is no longer shown in the middle of the screen on mobile
- when using the system color scheme and the system is using a dark theme, feed entries no longer flicker on load
- the demo account (if enabled) cannot register custom javascript code anymore
- removed the usage of `toSorted` in the client because older browsers do not support it (#1183)
- the openapi documentation is no longer cached by the browser so you always have access to the latest version
- added a memory management section to the readme, reading it is recommended if you are running CommaFeed on a server
  with limited memory
- fixed an issue that caused users without an email address set to be unable to edit their profile (#1184)

## [4.0.0]

- migrated from dropwizard 2 to dropwizard 4, Java 17+ is now required
- entries that were fetched and inserted in the database but not yet shown in the UI are no longer marked as read when
  marking all entries as read
- your custom sidebar width is now persisted in the local storage of your browser
- there is now a third color scheme option in addition to light and dark: system (follows the system color scheme)
- added support for youtube playlist favicons
- custom JS code is now executed when the app is done loading instead of when the page is loaded
- the favicon is now correctly returned for feeds that return an invalid content type
- the feed refresh engine now uses httpclient5 with connection pooling and no longer creates a new client for each
  request, reducing CPU usage
- updated UI library Mantine to 7.0, improving performance
- the h2 embedded database is now compacted on shutdown to reclaim unused space
- the admin connector on port 8084 is now disabled in config.yml.example. Disabling it in your config.yml is
  recommended (see https://github.com/Athou/commafeed/commit/929df60f09cce56020b0962ab111cd8349b271b0)
- migrated documentation from swagger 2 to openapi 3
- added a GET method to the fever api to indicate that the endpoint is working correctly when accessed from a browser
- the websocket connection can now be disabled, the websocket ping interval and the tree reload interval can now be
  configured (see config.yml.example)
- the websocket connection now works correctly when the context root of the application is not "/"
- unstable pubsubhubbub support was removed

## [3.10.1]

- swap next and previous buttons (#1159)
- unread count for subscriptions will now be shortened starting at 10k instead of 1k
- increased websocket ping interval to just under a minute to reduce data and battery usage on mobile
- only refresh subscription tree on a timer if websocket connection is unavailable
- the Docker image now uses less memory by returning unused memory to the OS
- add support for Java 21

## [3.10.0]

- added a Fever-compatible API that is usable with mobile clients that support the Fever API (see instructions in
  Settings -> Profile)
- long entry titles are no longer shortened in the detailed view
- added the "s" keyboard shortcut to star/unstar entries
- http sessions are now stored in the database (they were stored on disk before)
- fixed an issue that made it impossible to override the database url in a config.yml mounted in the Docker image

## [3.9.0]

- improve performance by disabling the loader when nothing is loading (most noticeable on mobile)
- added a setting to disable the 'mark all as read' confirmation
- added a setting to disable the custom context menu
- if the custom context is enabled, it can still be disabled by pressing the shift key
- the announcement feature is now working again and supports html ('announcement' configuration element in config.yml)
- add support for MariaDB 11+
- fix entry header shortly rendered as mobile on desktop, causing a small visual glitch
- fix an issue that could cause a feed to not refresh correctly if the url was very long
- database cleanup batch size is now configurable
- css parsing errors are no longer logged to the standard output
- fix small errors in the api documentation

## [3.8.1]

- in expanded mode, don't scroll when clicking on the body of the current entry
- improve content cleanup task performance for instances with a very large number of feeds

## [3.8.0]

- add previous and next buttons in the toolbar
- add a setting to always scroll selected entry to the top of the page, even if it fits entirely on screen
- clicking on the body of an entry in expanded mode selects it and marks it as read
- add rich text editor with autocomplete for custom css and js code in settings (desktop only)
- dramatically improve performance while scrolling
- fix broken welcome page mobile layout
- format dates in user locale instead of GMT in relative date popups

## [3.7.0]

- the sidebar is now resizable
- added the "f" keyboard shortcut to hide the sidebar
- added tooltips to relative dates with the exact date
- add a setting to hide commafeed from search engines (exposes a robots.txt file, enabled by default)
- the browser extension unread count now updates when articles are marked as read/unread in the app
- The "b" keyboard shortcut now works as expected on Chrome but requires the browser extension to be installed
- dark mode has been disabled on the api documentation page as it was unreadable
- improvement to the feed refresh queuing logic when "heavy load" mode is enabled
- fix a bug that could prevent feeds and categories from being edited

## [3.6.0]

- add a button to open CommaFeed in a new tab and a button to open options when using the browser extension
- clicking on the entry title in expanded mode now opens the link instead of doing nothing
- add tooltips to buttons when the mobile layout is used on desktop
- redirect the user to the welcome page if the user was deleted from the database
- add link to api documentation on welcome page
- the unread count is now correctly updated when using the "/next" bookmarklet while redis cache is enabled

## [3.5.0]

- add compatibility with the new version of the CommaFeed browser extension
- disable pull-to-refresh on mobile as it messes with vertical scrolling
- add css classes to feed entries to help with custom css rules
- api documentation page no longer requires users to be authenticated
- add a setting to limit the number of feeds a user can subscribe to
- add a setting to disable strict password policy
- add feed refresh engine metrics
- fix redis timeouts

## [3.4.0]

- add support for arm64 docker images
- add divider to visually separate read-only information from form on the profile settings page
- reduce javascript bundle size by 30% by loading only the necessary translations
- add a standalone donate page with all ways to support CommaFeed
- fix an issue introduced in 3.1.0 that could make CommaFeed not refresh feeds as fast as before on instances with lots
  of feeds
- fix alignment of icon with text for category tree nodes
- fix alignment of burger button with the rest of the header on mobile

## [3.3.2]

- restore entry selection indicator (left orange border) that was lost with the mantine 6.x upgrade (3.3.0)
- add dividers to visually separate read-only information from forms on feed and category details pages
- reduced javascript bundle size by 10%

## [3.3.1]

- fix long feed names not being shortened to respect tree max width

## [3.3.0]

- there are now database changes, rolling back to 2.x will no longer be possible
- restore support for user custom CSS rules
- add support for user custom JS code that will be executed on page load

## [3.2.0]

- restore the welcome page
- only apply hover effect for unread entries (same as commafeed v2)
- move notifications at the bottom of the screen
- always use https for sharing urls
- add support for redis ACLs
- transition to google analytics v4

## [3.1.0]

- add an even more compact layout
- restore hover effect from commafeed 2.x
- view mode (compact, expanded, ...) is now stored on the device so you can have a different view mode on desktop and
  mobile
- fix for the "Illegal attempt to associate a collection with two open sessions." error
- feed fetching workflow is now orchestrated with rxjava, removing a lot of code

## [3.0.1]

- allow env variable substitution in config.yml
- e.g. having a custom config.yml file with `app.session.path=${SOME_ENV_VAR}` will substitute `SOME_ENV_VAR` with its
  value
- allow env variable prefixed with `CF_` to override config.yml properties
- e.g. setting `CF_APP_ALLOWREGISTRATIONS=true` will set `app.allowRegistrations` to `true`

## [3.0.0]

- complete overhaul of the UI
- backend and frontend are now in separate maven modules
- no changes to the api or the database
- Docker images are now automatically built and available at https://hub.docker.com/r/athou/commafeed

## [2.6.0]

- add support for media content as a backup for missing content (useful for youtube feeds)
- correctly follow http error code 308 redirects
- fixed a bug that prevented users from deleting their account
- fixed a bug that made commafeed store entry contents multiple times
- fixed a bug that prevented the app to be used as an installed app on mobile devices if the context path of commafeed
  was not "/"
- fixed a bug that prevented entries from being "marked as read older than xxx" for a feed that was just added
- removed support for google+ and readability as those services no longer exist
- removed support for deploying on openshift
- removed alphabetical sorting of entries because of really poor performance (title cannot be indexed)
- improve performance for instances with the heavy load setting enabled by preventing CommaFeed from fetching feeds from
  users that did not log in for a long time
- various dependencies upgrades (notably dropwizard from 1.3 to 2.1)
- add support for mariadb
- add support for java17+ runtime
- various security improvements

## [2.5.0]

- unread count is now displayed in a favicon badge when supported
- the user agent string for the bot fetching feeds is now configurable
- feed parsing performance improvements
- support for java9+ runtime
- can now properly start from an empty postgresql database

## [2.4.0]

- users were not able to change password or delete account
- fix api key generation
- feed entries can now be sorted alphabetically
- fix facebook sharing
- fix layout on iOS
- postgresql driver update (fix for postgres 9.6)
- various internationalization fixes
- security fixes

## [2.3.0]

- dropwizard upgrade 0.9.1
- feed enclosures are hidden if they already displayed in the content
- fix youtube favicons
- various internationalization fixes

## [2.2.0]

- fix youtube and instagram favicon fetching
- mark as read filter was lost when a feed was rearranged with drag&drop
- feed entry categories are now displayed if available
- various performance and dependencies upgrades
- java8 is now required

## [2.1.0]

- dropwizard upgrade to 0.8.0
- you have to remove the "app.contextPath" setting from your yml file, you can optionally use
  server.applicationContextPath instead
- new setting app.maxFeedCapacity for deleting old entries
- ability to set filtering expressions for subscriptions to automatically mark new entries as read based on title,
  content, author or url.
- ability to use !keyword or -keyword to exclude a keyword from a search query
- facebook feeds now show user favicon instead of facebook favicon
- new dark theme 'nightsky'

## [2.0.3]

- internet explorer ajax cache workaround
- categories are now deletable again
- openshift support is back
- youtube feeds now show user favicon instead of youtube favicon

## [2.0.2]

- api using the api key is now working again
- context path is now configurable in config.yml (see app.contextPath in config.yml.example)
- fix login on firefox when fields are autofilled by the browser
- fix scrolling of subscriptions list on mobile
- user is now logged in after registration
- fix link to documentation on home page and about page
- fields autocomplete is disabled on the profile page
- users are able to delete their account again
- chinese and malaysian translation files are now correctly loaded
- software version in user-agent when fetching feeds is no longer hardcoded
- admin settings page is now read only, settings are configured in config.yml
- added link to metrics on the admin settings page
- Rome (rss library) upgrade to 1.5.0

## [2.0.1]

- the redis pool no longer throws an exception when it is unable to aquire a new connection

## [2.0.0]

- The backend has been completely rewritten using Dropwizard instead of TomEE, resulting in a lot less memory
  consumption and better overall performances.
  See the README on how to build CommaFeed from now on.
- CommaFeed should no longer fetch the same feed multiple times in a row
- Users can use their username or email to log in
