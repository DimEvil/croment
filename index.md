---
layout: workshop      # DON'T CHANGE THIS.
# More detailed instructions (including how to fill these variables for an
# online workshop) are available at
# https://carpentries.github.io/workshop-template/customization/index.html
venue: "Institute for Environment and Nature (Zavod za zaštitu okoliša i prirode) of the Ministry of Economy and Sustainable Development"        # brief name of the institution that hosts the workshop without address (e.g., "Euphoric State University")
address: "ZG Tower Annex, Big conference hall (Velika dvorana), 3rd floor, Radnička cesta 80, Zagreb"     # full street address of workshop (e.g., "Room A, 123 Forth Street, Blimingen, Euphoria"), videoconferencing URL, or 'online'
country: "HR"           # lowercase two-letter ISO country code such as "fr" (see https://en.wikipedia.org/wiki/ISO_3166-1#Current_codes) for the institution that hosts the workshop
language: "en"        # lowercase two-letter ISO language code such as "fr" (see https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) for the workshop
latitude: 45.800610   # decimal latitude of workshop venue (use https://www.latlong.net/)
longitude: 16.007450  # decimal longitude of the workshop venue (use https://www.latlong.net)
humandate: "February 19-23, 2024"    # human-readable dates for the workshop (e.g., "Feb 17-18, 2020")
humantime: "9:00 - 17:00 CET"    # human-readable times for the workshop e.g., "9:00 am - 4:30 pm CEST (7:00 am - 2:30 pm UTC)"
startdate: 2024-02-19      # machine-readable start date for the workshop in YYYY-MM-DD format like 2015-01-01
enddate: 2024-02-23        # machine-readable end date for the workshop in YYYY-MM-DD format like 2015-01-02
# instructor list : a boxed, comma-separated list of instructors' names as strings, like ["Abby Benson", "Mathew Biddle"]
instructor: [ "Dimitri Brosens", "André Heughebaert"]  
# helper list: a boxed, comma-separated list of helper's names as strings, like ["Ben Best", "Carolina Peralta"]
helper: ["Luka Katušić",
"Silvija Ajredini", 
"Petra Rodić",
"Gabrijela Šestani"
] 
email: ["d.brosens@biodiversity.be"]    # boxed, comma-separated list of contact email addresses for the host, lead instructor, or whoever else is handling questions, like ["marlyn.wescoff@example.org", "fran.bilas@example.org", "ruth.lichterman@example.org"]
collaborative_notes:  # optional: URL for the workshop collaborative notes, e.g. an Etherpad or Google Docs document (e.g., https://pad.carpentries.org/2015-01-01-euphoria)
eventbrite:           # optional: alphanumeric key for Eventbrite registration, e.g., "1234567890AB" (if Eventbrite is being used)
---

{% comment %} See instructions in the comments below for how to edit specific sections of this workshop template. {% endcomment %}

{% comment %}
HEADER

Edit the values in the block above to be appropriate for your workshop.
If the value is not 'true', 'false', 'null', or a number, please use
double quotation marks around the value, unless specified otherwise.
And run 'make workshop-check' *before* committing to make sure that changes are good.
{% endcomment %}


{% comment %}
{% endcomment %}


{% comment %}
Check DC curriculum
{% endcomment %}

{% if site.carpentry == "dc" %}
{% unless site.curriculum == "dc-astronomy" or site.curriculum == "dc-ecology" or site.curriculum == "dc-genomics" or site.curriculum == "dc-socsci" or site.curriculum == "dc-geospatial" %}
<div class="alert alert-warning">
It looks like you are setting up a website for a Data Carpentry curriculum but you haven't specified the curriculum type in the <code>_config.yml</code> file (current value in <code>_config.yml</code>: "<strong>{{ site.curriculum }}</strong>", possible values: <code>dc-astronomy</code>, <code>dc-ecology</code>, <code>dc-genomics</code>, <code>dc-socsci</code>, or <code>dc-geospatial</code>). After editing this file, you need to run <code>make serve</code> again to see the changes reflected.
</div>
{% endunless %}
{% endif %}

{% comment %}
Check SWC curriculum
{% endcomment %}

{% if site.carpentry == "swc" %}
{% unless site.curriculum == "swc-inflammation" or site.curriculum == "swc-gapminder" %}
<div class="alert alert-warning">
It looks like you are setting up a website for a Software Carpentry curriculum but you haven't specified the curriculum type in the <code>_config.yml</code> file (current value in <code>_config.yml</code>: "<strong>{{ site.curriculum }}</strong>", possible values: <code>swc-inflammation</code>, or <code>swc-gapminder</code>). After editing this file, you need to run <code>make serve</code> again to see the changes reflected.
</div>
{% endunless %}
{% endif %}

{% comment %}
EVENTBRITE

This block includes the Eventbrite registration widget if
'eventbrite' has been set in the header.  You can delete it if you
are not using Eventbrite, or leave it in, since it will not be
displayed if the 'eventbrite' field in the header is not set.
{% endcomment %}
{% if page.eventbrite %}
<strong>Some adblockers block the registration window. If you do not see the
  registration box below, please check your adblocker settings.</strong>
<iframe
  src="https://www.eventbrite.com/tickets-external?eid={{page.eventbrite}}&ref=etckt"
  frameborder="0"
  width="100%"
  height="280px"
  scrolling="auto">
</iframe>
{% endif %}


<h2 id="general">General Information</h2>

{% comment %}
INTRODUCTION

Edit the general explanatory paragraph below if you want to change
the pitch.
{% endcomment %}

In February, a full week of GBIF immersion will be organized in Croatia. Next to a GBIF community workshop, where we will learn on how GBIF works, we will also organize 2 full days on data cleaning and publication.
These 2 days (February 21 and 22th) are intended to be a hands-on workshop focused on mobilizing biological observation datasets to the <a href="https://gbif.org/">Global Biodiversity Information Facility (GBIF)</a> by helping data providers standardize their data using Darwin Core including species observations from any type of sampling methodologies (e.g. visual surveys, microscopy, imaging, telemetry). The other 3 days are dedicated to setting op the GBIF node in Croatia in the framework of the GBIF CESP CROMENT (Mentoring Croatia) project. This workshop is organized by a The Belgian Biodiversity Platform & the Croatian Institute for Environment and Nature & The Habitat Foundation. For more information on the Croment procject, [visit](https://www.gbif.org/project/CESP2023-006/croment) this website

<p class="d-flex justify-content-around align-items-center">
  <a href="https://mingor.gov.hr/">
    <img src="{{ '/assets/img/croatia.png' | relative_url }}" alt="Croatia" width="200">
  </a>
  <a href="https://biodiversity.be/">
    <img src="{{ '/assets/img/bbpf.jpg' | relative_url }}" alt="Belgian GBIF node" width="130">
  </a>
  <a href="https://www.gbif.org/programme/82219/capacity-enhancement-support-programme">
    <img src="{{ '/assets/img/cesp.PNG' | relative_url }}" alt="CESP" width="180">
  </a>
  <a href="https://www.gbif.org/">
    <img src="{{ '/assets/img/gbif.png' | relative_url }}" alt="GBIF" width="200">
  </a>
  <a href="https://www.thehabitatfoundation.org/">
    <img src="{{ '/assets/img/thf.PNG' | relative_url }}" alt="THF" width="160">
  </a>
  <a href="https://www.belspo.be">
    <img src="{{ '/assets/img/belspo.png' | relative_url }}" alt="Belspo" width="200">
  </a>
</p>

#### *Hands on Data Workshop*
What the data workshop will cover:

* Darwin Core and the required terms for GBIF.
* Typical data cleaning tasks needed to standardize the data.
* Getting your data into a final Darwin Core format.
* Common QA/QC steps, data enhancement, and validation tools.
* Required metadata information.
* How to get your data into the Integrated Publishing Toolkit..
* Tools that will help in all of the above processes.

The goal is that by the end of the workshop you will have a dataset in a final standardized state and shared to GBIF. We are hoping to address some of the identified blockers, including: lack of time, training, and specific formatting questions.

#### *some pictures*

<a href="https://www.biodiversity.be/">
    <img src="{{ '/fig/img7.JPG' | relative_url }}" alt="Group picture" width="800">
  </a>

<p class="d-flex justify-content-around align-items-center">
  <a href="https://mingor.gov.hr/">
    <img src="{{ '/fig/img6.jpg' | relative_url }}" alt="Hands on" width="200">
  </a>
  <a href="https://mingor.gov.hr/">
    <img src="{{ '/fig/img8.jpg' | relative_url }}" alt="Hands on" width="200">
  </a>
  <a href="https://mingor.gov.hr/">
    <img src="{{ '/fig/img9.jpg' | relative_url }}" alt="Stakeholder exercise" width="200">
  </a>
  <a href="https://mingor.gov.hr/">
    <img src="{{ '/fig/img10.jpg' | relative_url }}" alt="Nodes meeting" width="200">
  </a>
  <a href="https://mingor.gov.hr/">
    <img src="{{ '/fig/img11.jpg' | relative_url }}" alt="Hands on" width="200">
  </a>
</p>


We have a short time together therefore our focus will be hands-on work in breakout rooms using the dataset you bring to the workshop. We will not have many presentations and they will be relatively short. Instead we will have large portions of time for you to work on your data and ask questions when you hit a stumbling block. Therefore, if you do not have a dataset to work on you may not find this workshop a good use of your time.

If you would like to learn more about GBIF and a short rationale for sharing data to it, please watch this [three minute video](https://www.youtube.com/watch?v=HvS6sRVZbHo) and share them with those you want to work with to share data.
{% if site.carpentry == "swc" %}
{% include swc/intro.html %}
{% elsif site.carpentry == "dc" %}
{% include dc/intro.html %}
{% elsif site.carpentry == "lc" %}
{% include lc/intro.html %}
{% endif %}

{% if site.pilot %}
This is a pilot workshop, testing out a lesson that is still under development. The lesson authors would appreciate any feedback you can give them about the lesson content and suggestions for how it could be further improved.
{% endif %}

#### *GBIF community workshop*
What the GBIF community workshop will cover

* The GBIF governance
* GBIF nodes and the ECA network
* GBIF implementation plan and work programmes
* GBIF strategic framework
* GBIF community formum
* Development of a national data mobilization strategy for Croatia
* Global registry of scientific collections (GrSciColl)

In this workshop we will talk about how GBIF is organized globally as an infrastructure and how we can translate this in local practices. How a GBIF node is organized and how to setup a community around GBIF. How to communicate to stakeholders

#### *Hands on technical workshop*
What the technical workshop will cover

* How to admin an IPT
* How to customize IPT
* Hosted Portals, a simple portal solution based on GBIF services
* GRSCiColl (Global Registry of Scientific Collections)
* GBIF Registry

#### Some more pictures

<p class="d-flex justify-content-around align-items-center">
  <a href="https://mingor.gov.hr/">
    <img src="{{ '/fig/workshop1.jpg' | relative_url }}" alt="Croatia" width="300">
  </a>
  <a href="https://mingor.gov.hr/">
    <img src="{{ '/fig/workshop2.jpg' | relative_url }}" alt="Belgian GBIF node" width="300">
  </a>
  <a href="https://mingor.gov.hr/">
    <img src="{{ '/fig/workshop3.jpg' | relative_url }}" alt="CESP" width="300">
  </a>
  <a href="https://mingor.gov.hr/">
    <img src="{{ '/fig/workshop4.jpg' | relative_url }}" alt="Croatia" width="300">
  </a>
  <a href="https://mingor.gov.hr/">
    <img src="{{ '/fig/workshop5.jpg' | relative_url }}" alt="Belgian GBIF node" width="300">
  </a>
</p>

## Audience

The hands-on workshop is open for researchers, data curaters, data managers who have an interest in the publication of data on <a href="https://gbif.org/"> the Global Biodiversity Information Facility (GBIF)</a> 
The GBIF community workshop is on invitation only. However the material available on this website could be of interest for anyone who is developping a GBIF Node and community.

The workshop is organized in the CESP project CROMENT, a GBIF funded project on capacity building.

{% if site.carpentry == "swc" %}
{% include swc/who.html %}
{% elsif site.carpentry == "dc" %}
{% include dc/who.html %}
{% elsif site.carpentry == "lc" %}
{% include lc/who.html %}
{% endif %}

## Practical

{% comment %}
LOCATION

This block displays the address and links to maps showing directions
if the latitude and longitude of the workshop have been set.  You
can use https://www.latlong.net/ to find the lat/long of an
address.
{% endcomment %}
{% assign begin_address = page.address | slice: 0, 4 | downcase  %}
{% if page.address == "online" %}
{% assign online = "true_private" %}
{% elsif begin_address contains "http" %}
{% assign online = "true_public" %}
{% else %}
{% assign online = "false" %}
{% endif %}
{% if page.latitude and page.longitude and online == "false" %}
<p id="where">
  <strong>Where:</strong>
  {{page.address}}.
  Get directions with
  <a href="//www.openstreetmap.org/?mlat={{page.latitude}}&mlon={{page.longitude}}&zoom=16">OpenStreetMap</a>
  or
  <a href="//maps.google.com/maps?q={{page.latitude}},{{page.longitude}}">Google Maps</a>.
</p>
{% elsif online == "true_public" %}
<p id="where">
  <strong>Where:</strong>
  online at <a href="{{page.address}}">{{page.address}}</a>.
  If you need a password or other information to access the training,
  the instructor will pass it on to you before the workshop.
</p>
{% elsif online == "true_private" %}
<p id="where">
  <strong>Where:</strong> This training will take place online.
  The instructors will provide you with the information you will need to connect to this meeting.
</p>
{% endif %}

{% comment %}
DATE

This block displays the date and links to Google Calendar.
{% endcomment %}
{% if page.humandate %}
<p id="when">
  <strong>When:</strong>
  {{page.humandate}}.
  {% include workshop_calendar.html %}
</p>
{% endif %}

{% comment %}
SPECIAL REQUIREMENTS

Modify the block below if there are any special requirements.
{% endcomment %}
<p id="requirements">
  <strong>Requirements:</strong>
  {% if online == "false" %}
    Participants must bring a laptop with a
    Mac, Linux, or Windows operating system (not a tablet, Chromebook, etc.) that they have administrative privileges on.
  {% else %}
    <ul>
      <li>Must have a dataset to work on.</li>
      <li>Must have some R or Python experience.</li>
      <li>Must have a basic knowledge of GitHub.</li>
      <li>Participants must bring a laptop with R and RStudio or Python software installed.</li>
    </ul>
  {% endif %}
</p>

{% comment %}
ACCESSIBILITY

Modify the block below if there are any barriers to accessibility or
special instructions.
{% endcomment %}
<p id="accessibility">
  <strong>Accessibility:</strong>
{% if online == "false" %}
  We are committed to making this workshop
  accessible to everybody.  For workshops at a physical location, the workshop organizers have checked that:
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
</p>
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
  <strong>Contact:</strong>
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

{% comment %}
<p id="roles">
  <strong>Roles:</strong>
  To learn more about the roles at the workshop (who will be doing what),
  refer to <a href="https://carpentries.org/workshop_faq/#what-are-the-roles-of-everyone-participating-in-a-workshop">our Workshop FAQ</a>.
</p>
{% endcomment %}

{% comment %}
WHO CAN ATTEND?

If you would like to specify who can attend the workshop,
you can use the section below.

Move the 'endcomment' tag above the beginning of the following
<p> tag to make this section visible.

Edit the text to match who can attend the workshop. For instance:
- This workshop is open to affiliates to ABC university.
- This workshop is open to the public.
- If you are interested in attending this workshop, contact me@example.com
  for more information

<p id="who-can-attend">
    <strong>Who can attend?:</strong>
    This workshop is open to ....
</p>
{% endcomment %}

<hr/>

{% comment%}
CODE OF CONDUCT

<h2 id="code-of-conduct">Code of Conduct</h2>

<p>
Everyone who participates in Carpentries activities is required to conform to the <a href="https://docs.carpentries.org/topic_folders/policies/code-of-conduct.html">Code of Conduct</a>. This document also outlines how to report an incident if needed.
</p>

<p class="text-center">
  <a href="https://goo.gl/forms/KoUfO53Za3apOuOK2">
    <button type="button" class="btn btn-info">Report a Code of Conduct Incident</button>
  </a>
</p>
<hr/>
{% endcomment %}


{% comment %}
Collaborative Notes

If you want to use an Etherpad, go to

https://pad.carpentries.org/YYYY-MM-DD-site

where 'YYYY-MM-DD-site' is the identifier for your workshop,
e.g., '2015-06-10-esu'.

Note we also have a CodiMD (the open-source version of HackMD)
available at https://codimd.carpentries.org
{% endcomment %}
{% if page.collaborative_notes %}
<h2 id="collaborative_notes">Collaborative Notes</h2>

<p>
We will use this <a href="{{ page.collaborative_notes }}">collaborative document</a> for chatting, taking notes, and sharing URLs and bits of code.
</p>
<hr/>
{% endif %}


{% comment %}
SURVEYS - DO NOT EDIT SURVEY LINKS

<h2 id="surveys">Surveys</h2>
<p>Please be sure to complete these surveys before and after the workshop.</p>
{% if site.carpentry == "incubator" %}
<p><a href="{{ site.incubator_pre_survey }}">Pre-workshop Survey</a></p>
<p><a href="{{ site.incubator_post_survey }}">Post-workshop Survey</a></p>
{% elsif site.incubator_pre_survey or site.incubator_post_survey %}
<div class="alert alert-danger">
WARNING: you have defined custom pre- and/or post-survey links for
a workshop not configured for The Carpentries Incubator
(the value of `curriculum` is not set to `incubator` in `_config.yml`).
Please comment out the `incubator_pre_survey` and `incubator_post_survey` fields
in `_config.yml` or, if this workshop is teaching a lesson in the Incubator,
change the value of `carpentry` to `incubator`.
</div>
{% else %}
<p><a href="{{ site.pre_survey }}{{ site.github.project_title }}">Pre-workshop Survey</a></p>
<p><a href="{{ site.post_survey }}{{ site.github.project_title }}">Post-workshop Survey</a></p>
{% endif %}

<hr/>
{% endcomment %}

{% comment %}
SCHEDULE

Show the workshop's schedule.

Small changes to the schedule can be made by modifying the
`schedule.html` found in the `_includes` folder for your
workshop type (`swc`, `lc`, or `dc`). Edit the items and
times in the table to match your plans. You may also want to
change 'Day 1' and 'Day 2' to be actual dates or days of the
week.

For larger changes, a blank template for a 4-day workshop
(useful for online teaching for instance) can be found in
`_includes/custom-schedule.html`. Add the times, and what
you will be teaching to this file. You may also want to add
rows to the table if you wish to break down the schedule
further. To use this custom schedule here, replace the block
of code below the Schedule `<h2>` header below with
`{% include custom-schedule.html %}`.
{% endcomment %}

<h2 id="schedule">Schedule</h2>
__Times are in CET.__

Overview recordings of each lesson can be found in [this playlist](https://youtube.com/playlist?list=PLlgUwSvpCFS7zytaWbZ6f4Szm3PnpFj_J).

{% include custom-schedule.html %}

{% comment %}
Edit/replace the text above if you want to include a schedule table.
See the contents of the _includes/custom-schedule.html file for an example of
how one of these schedule tables is constructed.
{% endcomment %}

{% if site.pilot %}
The lesson taught in this workshop is being piloted and a precise schedule is yet to be established. The workshop will include regular breaks. Please [contact the workshop organisers](#contact) if you would like more information about the planned schedule.
{% endif %}

<hr/>




{% comment %}
SETUP

Delete irrelevant sections from the setup instructions.  Each
section is inside a 'div' without any classes to make the beginning
and end easier to find.

This is the other place where people frequently make mistakes, so
please preview your site before committing, and make sure to run
'tools/check' as well.
{% endcomment %}

<h2 id="setup">Setup</h2>

<p>
  To participate in a
  {% if site.carpentry == "swc" %}
  Software Carpentry
  {% elsif site.carpentry == "dc" %}
  Data Carpentry
  {% elsif site.carpentry == "lc" %}
  Library Carpentry
  {% endif %}
  workshop,
  you will need access to software as described below.
  In addition, you will need an up-to-date web browser.
</p>
<p>
  We maintain a list of common issues that occur during installation as a reference for instructors
  that may be useful on the
  <a href = "{{site.swc_github}}/workshop-template/wiki/Configuration-Problems-and-Solutions">Configuration Problems and Solutions wiki page</a>.
</p>

{% comment %}
For online workshops, the section below provides:
- installation instructions for the Zoom client
- recommendations for setting up Learners' workspace so they can follow along
  the instructions and the videoconferencing

If you do not use Zoom for your online workshop, edit the file
`_includes/install_instructions/videoconferencing.html`
to include the relevant installation instrucctions.
{% endcomment %}
{% if online != "false" %}
{% include install_instructions/videoconferencing.html %}
{% endif %}

{% comment %}
These are the installation instructions for the tools used
during the workshop.
{% endcomment %}

{% if site.carpentry == "swc" %}
{% include swc/setup.html %}
{% elsif site.carpentry == "dc" %}
{% include dc/setup.html %}
{% elsif site.carpentry == "lc" %}
{% include lc/setup.html %}
{% elsif site.carpentry == "incubator" %}
Please check the "Setup" page of
[the lesson site]({{ site.incubator_lesson_site }}) for instructions to follow
to obtain the software and data you will need to follow the lesson.
{% endif %}
