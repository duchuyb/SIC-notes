# SIC tool (GUI) -- Latest version: V1.2.22 -- 30/06/2025 -- DB

A python program I designed to detect multiple interferences (Firewall/WAF/IDS/Load Balancer/CDN) <br />
This is the GUI version of the my original tool - **NOW** has a docker release.

# Features:  
- Configuration File: A centralised configuration system that provides flexibility for enabling or disabling features.
- Logs: Each script run saves logs in the `/logs/` directory, complete with date and time stamps.
- SSH Capabilities: This feature allows direct command execution on the hub via SSH.
- Wafw00f Integration: A valuable tool for detecting Web Application Firewalls (WAF).
- NMap Utility: Incorporated for local and hub usage, including WAF scripts.
- cURL Requests with Redirects: This feature attempts to make cURL requests from the hub and follows any redirects.
- Load Balancer detection: It works by making multiple HTTP requests to the target website and checking if the responses come from different IP addresses
- CDN detection: uses a combination of forward DNS lookup/rDNS lookup and observations around requests/responses
- Customisable Banner: Allows you to insert your banner for improved aesthetics.
- [Alpha] Experimental Features: An option to enable or disable experimental features, allowing you to insert preconfigured payloads to analyse WAF/IDS/Firewall behaviour.
- [Alpha] Blocking Features and Proxy Support: Offers detection capabilities for full and partial blocks.
- [Alpha]->[BETA] Rate-Limiter Detection: An algorithm designed to send multiple requests to observe any changes in HTTP responses.
- [Alpha]->[BETA] Running Custom Commands: This feature aims to execute commands on the hub and can run multiple commands.
- [Alpha] Concurrency Across Multiple Hubs: This capability has the potential to run algorithms against multiple hubs simultaneously.
- [Alpha] Detailed Log Viewer: This would allow you to filter specific tests and outputs.
- Many more features are available.

# *(30/06/2025)* Official Release (v1.2.22)
- ✅**Modded**: Reworked the rate-limiting function(s) completely. It now aggressively (supports concurrency) attempts to flood via port state polling (locally) and HTTP request flooding (on the internal hub.
- ✅**Modded**: Reduced the NMap delays to be quicker/more aggressive.
- ✅**Modded**: Settings.ini: Refactored for better visibility and structure, other than having everything under [General]
- ✅**Modded**: Adjusted when the NMap logs are outputted -> it is more appropriate when it finds the interference.
- ✅**Modded**: Experimental Feature logic completely revamped - test will stop once WAF behaviour is detected and a small report is generated.
- ✅**Added**: The additional option of blocked in the config file -> toggle on/off if you want this check to happen.
- ✅**Added**: Additional config changes to reflect on the rate-limitng option (both internal and external).
- ✅**Added**: An additional check for OS fingerprinting to the existing NMap checks, although it is likely only going to apply to the External NMap check.
- ✅**Added**: An additional check (during the CDN) for headers relating to rate-limit.
- ✅**Added**: The option for the user to set the limit to the rate limit.
- ✅**Added**: Basic Auth - The option of providing the username/password or the encoded base64.
- ✅**Added**: Colour coded messages in the terminal to reflect when things are successful and unsuccessful.
- ✅**Fixed**: the asyncio errors that occurs when you abort the program abruptly.
- ✅**Fixed**: the errors coming from CDN/Load balancer checks when data isn't available.
- ✅**Fixed**: the load balancer so it should now output IPs correctly.
- ✅**Fixed**: SSH logic where it now attempts to use WSL locally but SSH agents in the docker image.
- ✅**Fixed**: An issue where Nmap wasn't found because of windows. This now checks local WSL but in the docker image, this is a none problem.
- ✅**Fixed**: DNS lookup bug when it detected a name or service not known, this should no longer be outputted.
- ✅**Fixed**: Experimental Feature now works with the introduction of GUI.
- ✅**Fixed**: Race-condition issue that stopped the 'About' and 'Detailed Log Viewer from loading up.
- ✅**Fixed**: The modify custom commands button now works in the docker implementation.
- ✅**Fixed**: No longer outputs many messages when DNS lookup fails to resolve.

# GUI Changes
- ✅**Added**: The GUI has now been implemented to utilise a GUI to output the findings, along with configurable changes on the UI (Credit goes to Siji for the suggestion)
- ✅**Added**: Additional buttons (other than run scans), such as save config, modifying banner etc.
- ✅**Added**: labels, loads info from settings.ini and allows you to modify those changes.
- ✅**Added**: Icons appearing on the GUI application.
- ✅**Added**: Dark/Light mode is adapted to windows settings.
- ✅**Added**: introduce a clear button.
- ✅**Added**: Implementation of a Status bar (effectively based on the settings.ini).
- ✅**Added**: Client-Side Input Validation.
- ✅**Added**: Visual Grouping of Settings.
- ✅**Added**: Easter egg - A non-existant magic button.
- ✅**Added**: About me popup to include the logs of the latest update patch.
- ✅**Added**: Completely revamped the summary in the form of a pop.
- ✅**Added**: Emojis in the Scan Summary popup.
- ✅**Added**: Added recommendation, scan checklist and scan verdict in the Scan Summary popup.
- ✅**Added**: Colour coding to the Scan Summary popup.
- ✅**Added**: Grouped tests, along with collapsible grouping.
- ✅**Added**: Colour coded messages in the GUI to reflect when things are successful and unsuccessful.
- ✅**Added**: Introduction to the detailed log viewer, where we can view the logs of each individual test.
- ✅**Fixed**: Fixed GUI problem where the labels and main properties (logs, config) weren't scaling properly.
- ✅**Removed**: The load from settings.ini option entirely.
- ✅**Modded**: Improved logic for the target port, to be more intuitive.
- ✅**Modded**: The run scan button to change to "stop scan" when the scan is running.
- ✅**Modded**: Removed the customise banner for viewing Scan summary pop-up.
- ✅**Modded**: The layout of the buttons so the run scan is bigger and we can compensate for the newly designed detailed log viewer.

# To-Do List - next release
- ✅ [SSH Rate Limit Test] Allow user to set the limit for HTTP flood test.
- ✅ [Grouped Settings] an option to expand the view of the options.
- ✅ [SSH Hub IP] Modify this to be a dropdown menu of which hub instead.
- ✅ [Logs] Fix logs not being outputted on docker.
- ✅ [Ping Test] Refactored this to be a [Reachability Test] as Ping can be unreliable at times.
- ✅ [cURL Test] Resolve some rate limit logic, improved the logic for detecting rate limit headers.
- [SSH Rate Limit Test] Set a hard limit to local rate limit to 1000, unless you set a flag.
- [Modify Commands] Error relating to [_tkinter.TclError: grab failed: another application has grab].
- [View Detailed logger] Include more filters in the Viewed detailed logs like payload tests and more.
- [View Scan Summary] Modify the summary popup - for the grouped status, it can be confusing.
- [View Scan Summary] Modify the status messages - either all of them have fixed sizes or limit the messaging.
- [General] Tooltip popup that appears in each option.
- [General] Unselecting SSH tests should disable other options.
- [Local Rate limit Test] Add multiple ports to run the port state polling against.
- [Modify custom commands button] (pluma:9): dbind-WARNING **: 08:53:31.084: AT-SPI: Error retrieving accessibility bus address: org.freedesktop.DBus.Error.ServiceUnknown: The name org.a11y.Bus was not provided by any .service files
- [Stop button] Investigate the delay with "stopping..."
- [Expanding buttons] Idea is possibly replacing the modify commands to an expansive option instead.
- [Customise banner] Bring this back.
- [About Me Pop-up] the scroll is not immediately scrollable with the mouse roller.
- [About me Pop-up] Will need to adapt the default size (make larger).
- [Targets website option] Copying and pasting doesn't replace the entire text
- [NMAP local and SSH] - can sometimes get stuck, needs to timeout sooner.
