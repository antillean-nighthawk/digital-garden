---
{"dg-publish":true,"permalink":"/content/osint/","tags":["osint","ctf"],"created":"2024-09-16T18:19:15.722-07:00","updated":"2024-09-16T18:43:25.584-07:00"}
---



> [!NOTE] Note
Everything here should be free or freemium. Some services may require an account but it is useful to make some sockpuppets (fake accounts) specifically for OSINT purposes. Despite the info being available on the clear web, it is still a good idea to use a virtual machine and sockpuppet accounts so the investigation cannot be traced back to you.
## Multipurpose

| Website                                         | Email | Username | IP | Name | Phone | Hash | Co | URL |
|-------------------------------------------------|-------|----------|----|------|-------|------|----|-----|
| https://www.virustotal.com/                     |       |          | x  |      |       | x    |    | x   |
| https://www.shodan.io/                          | x     |          | x  |      |       |      | x  | x   |
| https://pulsedive.com/                          |       |          | x  |      |       |      |    | x   |
| https://hunter.io/                              | x     |          |    |      |       |      | x  | x   |
| https://talosintelligence.com/reputation_center |       |          | x  |      |       | x    | x  | x   |
| https://www.wappalyzer.com/                     | x     |          |    |      |       |      | x  | x   |
| https://epieos.com/                             | x     |          |    |      | x     |      |    | x   |
| https://builtwith.com/                          |       |          |    |      |       |      | x  | x   |
| https://whatsmyname.app/                        | x     | x        |    | x    |       |      |    |     |
| https://rocketreach.co/                         | x     |          |    | x    | x     |      | x  |     |
| https://threatfox.abuse.ch/browse/              |       |          | x  |      |       | x    |    | x   |
| https://lookup.icann.org/                       |       |          | x  |      |       |      |    | x   |
| https://otx.alienvault.com/                     | x     |          | x  |      |       | x    | x  | x   |
| https://breachdirectory.org/                    | x     | x        |    |      |       |      |    |     |

## DNS
- `dig <domain> <type of record>`
- https://www.nslookup.io/
- https://dnsdumpster.com/
- https://viewdns.info/
- https://mxtoolbox.com/
- https://securitytrails.com/
- https://www.urlvoid.com/
- https://urlscan.io/

## IP lookup
- `whois`
- https://www.abuseipdb.com/
- https://ipinfo.io/ 
- https://www.ipqualityscore.com/
- https://www.ipvoid.com/
- https://browserleaks.com/
- https://search.censys.io/
- https://viz.greynoise.io/

## Breaches and leaks
- https://dehashed.com/ 
- https://wikileaks.org/
- https://intelx.io/
- https://haveibeenpwned.com/
- https://ddosecrets.com/

## Specific sites
- open FTP index: https://www.mmnt.net/
- live cams: http://www.insecam.org/

## Other people's OSINT collections
there's way wayyyy more stuff out there, mostly on start.me or Github
- https://start.me/p/DPYPMz/the-ultimate-osint-collection
- https://start.me/p/7kxyy2/osint-tools-curated-by-lorand-bodo
- https://start.me/p/VRxaj5/dating-apps-and-hook-up-sites-for-investigators
- https://start.me/p/m6XQ08/osint
- https://start.me/p/ZME8nR/osint
- https://start.me/p/rxeRqr/aml-toolbox?embed=1
- https://github.com/jivoi/awesome-osint
- https://github.com/Ph055a/OSINT_Collection#ph055as-osint-collection
- https://bit.ly/bcattools
- https://osintframework.com/
- https://www.osintdojo.com/resources/
- https://www.osintcombine.com/free-osint-tools/osint-bookmark-stack
- [Intel Techniques](https://inteltechniques.com/tools/index.html) has a large repo of search tools

## Angles to consider
- social medias: Reddit, Facebook, IG, Twitter, TikTok, Snapchat, etc.
- review sites: TripAdvisor, Yelp, Glassdoor, BBB, TrustPilot, etc.
- dating sites: Tinder, Grindr, Hinge, eHarmony, Bumble, OkCupid, etc.
- public filings: patents, SEC reports, licenses, criminal records, contracts, court orders
- job sites: company website or socials, directories, job postings
	- job boards (LinkedIn, Indeed, Handshake, Monster, etc.)
- search engines: [Google dorking](https://www.exploit-db.com/google-hacking-database)
	- country specific search engines (Baidu, Yandex, etc.)
	- topic specific search (Github, FlightAware, VintageFashionGuild, etc)
- publications: research papers, newspapers/sites, gray literature, blogs, whitepapers
- geospatial: Google Earth, maps/satellite, reverse image search, languages, landmarks, weather, flora/fauna
- historial artifacts: Wayback Machine, Internet Archive, cached pages, screenshots/images