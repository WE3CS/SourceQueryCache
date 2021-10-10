# Source Query Cache #
Original plugin: https://forums.alliedmods.net/showthread.php?t=135543
rewroted by energie4cute:https://forums.alliedmods.net/showpost.php?p=2159684&postcount=41

06-30-14 , 08:55 AM   Re: Metamod Query Cache
Reply With Quote #41
I've rewrote the extension ( cleaned up the code mostly ). The main thing I added was a RequestMap.
Now each time a A2S_INFO request is received, the IP it's added into a map. If the client sends more than qc_maxrequests per second he no longer receives the A2S_INFO responses in that second ( can be changed to a more severe behaviour if needed ). This could be done even better by peaking at the data just to check the IP and save some time that is used while the buffer is moved, but I have yet to search for some more info about the Valve networking code ( noob here ).

The only builds I made were CSGO,CSS,L4D,L4D2,TF2,SDK2013.

If anyone wants to build it : link

CVars :
- qc_time - A2S_INFO requests timeout in seconds.
- qc_maxrequests - Maximum ammount of A2S_INFO requests per second. ( RequestMap must be enabled for this to work )
- qc_requestmap_enabled - Enable/disable the RequestMap. Will rehook recvfrom ( I wanted to keep it optimized and this is better than checking if the RequestMap is enabled each time recvfrom is called )

Commands :
- qc_requestmap - Prints the RequestMap.
- qc_requestmap_clear - Clears the RequestMap. ( auto @ plugin_un/load / map_load )

How to install :
Quote:
Let's say you want to install it on a Linux CSS Server :
You copy qcache_mm.vdf into addons/metamod
You copy linux/qcache_mm.css/qcache_mm.so into addons/

Same rules apply to other servers.
Edit : Reuploaded new version. Should load now on Linux
Edit2 : Uploaded version 1.0.0.1. ( Added qc_requestmap_enabled and remade qc_requestmap a bit, now it shows the traffic done : total requests in that second and the total overlimits for all-time ). Also did some tests and it seemed pretty ok for low amounts of traffic ( 30 A2S_INFO requests per second ).
Edit3 : Recompiled.
Edit4 : Added SDK2013 version.
