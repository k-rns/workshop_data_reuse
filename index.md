---
layout: lesson
root: .  # Is the only page that doesn't follow the pattern /:path/index.html
permalink: index.html  # Is the only page that doesn't follow the pattern /:path/index.html
venue: "Woods Hole Oceanographic Institution"        # brief name of the institution that hosts the workshop without address (e.g., "Euphoric State University")
address: "On-line"               # full street address of workshop (e.g., "Room A, 123 Forth Street, Blimingen, Euphoria"), videoconferencing URL, or 'online'
country: "us"                    # lowercase two-letter ISO country code such as "fr" (see https://en.wikipedia.org/wiki/ISO_3166-1#Current_codes) 
language: "en"                   # lowercase two-letter ISO language code such as "fr" (see https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) for the workshop
latitude: "41.526730"            # decimal latitude of workshop venue (use https://www.latlong.net/)
longitude: " -70.663184"         # decimal longitude of the workshop venue (use https://www.latlong.net)
humandate: "Oct 27, 2021"        # human-readable dates for the workshop (e.g., "Feb 17-18, 2020")
humantime: "8:30 - 12:30 EST"    # human-readable times for the workshop e.g., "9:00 am - 4:30 pm CEST (7:00 am - 2:30 pm UTC)"
startdate: 2021-10-27            # machine-readable start date for the workshop in YYYY-MM-DD format like 2015-01-01
enddate: 2021-10-27              # machine-readable end date for the workshop in YYYY-MM-DD format like 2015-01-02
instructor: ["Karen Soenen"]      # boxed, comma-separated list of instructors' names as strings, like ["Kay McNulty", "Betty Jennings", "Betty Snyder"]
helper: ["Amber York", "Stace Beaulieu"]     # boxed, comma-separated list of helpers' names, like ["Marlyn Wescoff", "Fran Bilas", "Ruth Lichterman"]
email: ["ksoenen@whoi.edy","stace@whoi.edu", "adyork@whoi.edu"]    # boxed, comma-separated list of contact email addresses for the host, lead instructor
collaborative_notes:  # optional: URL for the workshop collaborative notes, e.g. an Etherpad or Google Docs document (e.g., https://pad.carpentries.org/2015-01-01-euphoria)
eventbrite:           # optional: alphanumeric key for Eventbrite registration, e.g., "1234567890AB" (if Eventbrite is being used)
---



---
FIXME: home page introduction

<!-- this is an html comment -->

{% comment %} This is a comment in Liquid {% endcomment %}

> ## Prerequisites
>
> FIXME
{: .prereq}

{% include links.md %}
