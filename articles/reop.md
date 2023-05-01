---
layout: page
permalink: "/articles/reop"
title: "Reop-Mode"
---
In ircd 2.11.0 the Reop-Mode has been introduced to IRCnet. When a channel becomes opless, one of the users matching the added hostmasks will be opped after a delay.

Like ban, invite and exception  list, the reop list contains hostmasks in format ```nick!ident@host.```

Retrieve the reop list:
```MODE #channel R```

```
:irc.example.com 344 nick #channel *!user1@ircnet.com
:irc.example.com 344 nick #channel *!user2@ircnet.com
:irc.example.com 345 nick #channel :End of Channel Reop List
```

Add reop entries:
```
MODE #channel +R *!user@ircnet.com
```

Remove reop entries:
```
MODE #channel -R *!user@ircnet.com
```

When the channel became opless, reop will be enforced after 90 minutes:
```
:irc.example.com NOTICE #channel :Enforcing channel mode +R (166)
:irc.example.com MODE #channel +o nick
```

## Hints
* Keep your reop entries up to date (domain expired? shell account closed?)
* Be careful with wildcards. Never use wildcards like ```*!user@151.141.187.*``` because they can be spoofed easily, e.g. ```*!user@151.141.187.ircnet.com```. Use CIDR notation instead: ```*!user@151.141.187.0/24```.
* Reop entries can be restricted to countries by using ISO-3166-1 country codes. E.g. ```276*!user@ircnet.com``` will reop only users on *.DE IRCnet servers.
* If the channel is opless, users matching the reoplist are allowed to join the channel by overriding the channel limit.
* If the channel is empty, reops will get lost, like all other channel information
* If the server is currently in split-mode (maybe even due to misconfiguration), you will not get opped. To test that check if you get op when you join a non-existing channel.

<br><br>
© IRCnet.com




