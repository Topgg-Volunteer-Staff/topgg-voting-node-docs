---
description: Webhooks require special considerations when running them from a home network.
---

# Running webhooks from home

Webhooks will require the ability for Topgg to be able to reach your computer via http requests. Since your home network isn't quite setup in the same way as a VPS or other hosts it will require some special configuration.

### Port forwarding

If you try to host a webhook at home without port forwarding your home router will not know which device to send the request to. You'll need to tell it what port your webhook is on, and which computer will handle them.\
\
Every router is different so you may want to visit [https://portforward.com/router.htm#1](https://portforward.com/router.htm#1) for more information.

### Dynamic IP's

Many internet service providers around the world will change your home public IP from time to time. Your public IP will be required for hosting webhooks from home, if your ISP changes your IP frequently its probably not a good idea to host from home. You may need to contact your ISP to request a static IP.

### Finding your public IP

You can find your public IP by opening any web browser with all VPN's disabled and searching "What is my ip address" in your preferred search engine.
