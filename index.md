---
layout: lesson
root: .  # Is the only page that doesn't follow the pattern /:path/index.html
permalink: index.html  # Is the only page that doesn't follow the pattern /:path/index.html
---


{% comment %}
GENERAL INTRODUCTION
Modify the block below if there are any special requirements.


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
{% endcomment %}


{% comment %}
HEADER
Edit the values in the block above to be appropriate for your workshop.
If the value is not 'true', 'false', 'null', or a number, please use
double quotation marks around the value, unless specified otherwise.
And run 'make workshop-check' *before* committing to make sure that changes are good.
{% endcomment %}


<h2 id="general">General Information</h2>

Workshops always have the cleanest, best examples of data tables to use, don't they? These tables always seem to be immediately usable for analysis. Getting a raw table usable for analysis is a process called "data wrangling". In this workshop we'll show you how to get to this perfect table using Python and the package Pandas. 

Doing this process correctly will not only make you more efficient, but it will also make your data easier to reuse in the future. 

The workshop is sponsored by a WHOI Academic Programs Doherty Award and a DDVPR Technical Staff Training Award


<p>
  <strong>Who:</strong>
  This workshop is targeted towards improving project efficiency and building technical skills.
The workshop will only be held for 10 people at a time through an online Zoom meeting. 
  Registration is required. Please contact <a href = "mailto: stace@whoi.edu">stace@whoi.edu</a> for availability.
</p> 

<p id="requirements">
  <strong>Requirements:</strong> 
  <ul>
    <li>Participants must bring a laptop with a Mac, Linux, or Windows operating system (not a tablet, Chromebook, etc.) that they have administrative privileges on.</li>
    <li>A few specific software packages need to be installed (listed in the "Setup page" <a href="#setup">below</a>). We will be holding an on-line data lab to help you install these packages if necessary.</li>
    <li> Participants will need to join a Zoom video conference. Installing free zoom conference software is recommended.  You will not need a paid account. See <a href="https://support.zoom.us/hc/en-us/articles/201362193-Joining-a-Meeting">Joining a meeting from Zoom Help Center</a></li>
    <li>This is an introduction to Python and data tables designed for participants with no programming experience.
</li>
   </ul>   
</p>
 
<p id="accessibility">
  <strong>Accessibility:</strong>
{% if online == "false" %}
  We are committed to making this workshop
  accessible to everybody. The workshop organizers have checked that:
</p>
<ul>
  <li>The room is wheelchair / scooter accessible.</li>
  <li>Accessible restrooms are available.</li>
</ul>
<p>
  Materials will be provided in advance of the workshop and
  large-print handouts are available if needed by notifying the
  organizers in advance.  If we can help making learning easier for
  you (e.g. sign-language interpreters, lactation facilities) please
  get in touch (using contact details below) and we will
  attempt to provide them.
{% else %}
  We are dedicated to providing a positive and accessible learning environment for all. Please
  notify the instructors in advance of the workshop if you require any accommodations or if there is
  anything we can do to make this workshop more accessible to you.
</p>
{% endif %}

{% comment %}
CONTACT EMAIL ADDRESS

Display the contact email address set in the configuration file.
{% endcomment %}
<p id="contact">
  <strong>Contact</strong>:
  Please email
  {% if page.email %}
  {% for email in page.email %}
  {% if forloop.last and page.email.size > 1 %}
  or
  {% else %}
  {% unless forloop.first %}
  ,
  {% endunless %}
  {% endif %}
  <a href='mailto:{{email}}'>{{email}}</a>
  {% endfor %}
  {% else %}
  to-be-announced
  {% endif %}
  for more information.
</p>

<hr/>


<h2 id="why-wrangling">Am I a data wrangler?</h2>
The process called "data wrangling", i.e., manipulating data into a usable form and diagnosing data quality issues often constitutes the most tedious and time-consuming aspect of analysis. 


<p>
<center>
<figure>
  <a href="https://doi.org/10.1177/1473871611415994" target="_blank"><img src="https://www.researchgate.net/profile/Paolo_Buono/publication/261843443/figure/fig1/AS:296928958009345@1447804788361/The-iterative-process-of-wrangling-and-analysis-One-or-more-initial-data-sets-may-be.png" alt="Regular expression xkcd comic" style="width:60%">
  <figcaption>Kandel, S. et al (2011). Research directions in data wrangling: Visualisations and transformations for usable and credible data. Inf. Vis., 10(4),271-288</figcaption>
</a>
</figure>
</center>
</p>

<p>This workshop is for you if you:</p> 
<ul>
  <li>are working with tabular/time series data.</li>
  <li>want to decrease the amount of manual work on your dataset like searching, cutting & pasting, correcting systematic errors, etc.</li>
  <li>want to perform statistical analysis and plots</li>
  <li>want to increase the value of your dataset for re-use and collaboration.</li>
</ul>   

<hr/>

<h2 id="code-of-conduct">Code of Conduct</h2>

<p>We will be using the Carpentries code of conduct for this workshop.</p>
<p>Everyone who participates in this workshop is required to conform to the <a href="https://docs.carpentries.org/topic_folders/policies/code-of-conduct.html">Code of Conduct</a>. 
</p>


<hr/>


{% comment %}
SURVEYS - DO NOT EDIT SURVEY LINKS
{% endcomment %}
<h2 id="surveys">Surveys</h2>
<p>Please be sure to complete these surveys before and after the workshop.</p>
<p><a href="{{ site.pre_survey }}{{ site.github.project_title }}">Pre-workshop Survey</a></p>
<p><a href="{{ site.post_survey }}{{ site.github.project_title }}">Post-workshop Survey</a></p>

<hr/>


This workshop is based on a few workshops developed by the Carpentries (See <a href="https://carpentries.org">https://carpentries.org</a>  for more information about the Carpentries organisation.) and by Joe Futrelle (WHOI):
<ul>
  <li><a href=" https://datacarpentry.org/spreadsheet-ecology-lesson/">Data Organization in Spreadsheets for Ecologists</a></li>
  <li><a href="https://datacarpentry.org/python-ecology-lesson/">Data Analysis and Visualization for Ecologists</a></li>
  <li><a href="https://github.com/WHOIGit/pandas-talk/">Python and the Pandas package-Joe Futrelle (WHOI)</a></li>
</ul>

<br>


> ## Prerequisites
>
> FIXME
{: .prereq}

{% include links.md %}
