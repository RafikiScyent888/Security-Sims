# Parked: a router access-list fault sim (not named, not built)

Stored 6 November 2026 at the owner's request: "I need you to save this as a new sim for security. store
this for now. We will have to name this and add stuff to it to make sure that it teaches what it needs to
without it being a straight copy from the comptia website. store it for now."

**Status: parked.** Nothing is built, nothing is on the dashboard, nothing is live. It gets a name and its
own content after the owner talks it through.

**Where it came from:** CompTIA's public example simulation, from five screenshots the owner sent. The
screenshots are CompTIA's material, so they are kept privately, not in this public repo (the standing
instructions say where).

## What the example does (described in our own words, not copied)

- **The network:** a small company behind one router, in three parts: the staff network (two workstations,
  a printer, a switch), a screened subnet (DMZ) holding the DNS, file, email and web servers, and the
  provider's link to the internet. The two inside parts are /27s side by side; the provider link is a /30.
- **The router's access list:** ten rules, read top to bottom, ending in a deny for everything. Most are
  security the company meant to have: staff may reach the DMZ; SSH and RDP out are blocked; the web
  servers take HTTP and HTTPS from anywhere; pings into the DMZ are blocked; staff can't send SNMP or mail
  straight out; then staff may go anywhere else. One rule doesn't belong: a deny for everything from a /28
  that sits inside the staff /27, placed above the staff's "go anywhere" rule.
- **The fault:** one executive's PC has an address inside that /28. It still prints (the printer is on its
  own network, so nothing crosses the router), and still reaches internal email and the intranet (the
  earlier staff-to-DMZ rule matches first). But every packet for the internet meets the /28 deny before it
  reaches the staff's allow rule. The other workstation, in the lower half of the /27, gets out.
- **What the student does:** `ipconfig` and `ping` on each workstation (their terminals know only those
  and `exit`); read the router's interfaces and its list; change only what fixes it, which is to remove the
  one rule, leaving every security rule around it in place.

## What it teaches (to check against the owner's "All updated Objectives" doc, Security+ V8, when built)

- Firewall and router access lists are read top to bottom, and the first rule that matches decides.
- A subnet inside a subnet: a /28 is half of a /27, so a rule for it catches only some of the staff.
- The deny at the end, and why "deny everything else" is there.
- A screened subnet (DMZ) and the rules that guard it.
- Troubleshooting from the symptoms: what still works (printing, email, intranet) rules things out and points
  at the path that doesn't.
- Least change: fix the fault without opening up anything the security rules close.

## To talk out before building, so it is the program's own

- Its name.
- Its own business, story, network, addresses and device names (not the example's company or addresses).
- More than one fault, so it can't be memorised: the stray /28 deny, a rule in the wrong order, a wrong
  port or protocol, DNS blocked so names fail while addresses work, a mask that covers too much or too
  little; with the student saying why each security rule must stay.
- The program's rules: unlimited tries; hints on the three-rung ladder that never give the answer; where
  the student chooses, six options (one right, five near misses) with a wrong pick going red and staying
  red, marked three ways; AAA contrast on painted pixels; easier reading that persists; five extra
  scenarios; the dashboard tile, the Back to Dashboard bar and the program's footer; a 3D model if one is
  wanted (the router, the rack).
- How it sits beside the existing Firewall ACL PBQ (`firewall-acl-pbq.html`), which has students read a
  rule table (true or false, spot the issues) rather than troubleshoot a live fault.
