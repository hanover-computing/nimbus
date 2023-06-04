# Nimbus
> An HTTP(S) proxy that transparently handles scraping protection bypass, IP rotation, security, etc.

## Project Goals
Applications that send out HTTP/HTTPS requests in one form or another (whether it be plain requests a la curl/got, or through Puppeteer/Playwright and simulating a full user session) all need to do a whole host of things that aren't even related to the application logic:
- bypassing scraping protection
  - IP rotation
  - IP reputation management
  - request pattern management
  - respecting robots.txt
  - captcha solving
- figuring out request status (blocked/404/captcha/internal error/etc)
- securing requests from hitting internal services (SSRF)
- and so much more!

The idea is to have a proxy layer that transparently and automatically handles all of the above, so that the applications making the requests don't even have to think about it.

The plan is to have a bare-bones HTTP(S) proxy with a pluggable architecture, where the individual "features" can either be implemented as an internal plugin that comes bundled with the repo, or to have plugins that interface and integrate with external libraries/services, such as using [got-ssrf](https://github.com/hanover-computing/got-ssrf) to get SSRF protection for "free".
