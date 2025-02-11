# Original event logs

Events were recorded onboard with Rolling Deck to Repository (R2R) event
logger (elog) software described at:
https://www.rvdata.us/about/event-log. Prior to each cruise an NES-LTER
Information Manager works with shipboard technicians and the R2R elog
software team to configure the elog with instruments and actions from a
controlled vocabulary. The event log is started when the ship leaves
port, and concluded upon arrival. During the cruise the events are added
manually by shipboard technicians and science party. Contents of the
event log are reviewed regularly by an on-board Information Manager
during a cruise to ensure completeness and accuracy. The elog is often
available online during the cruise so that an on-shore Information
Manager can review contents as well. The original event logs (elogs) are
available per cruise in R2R with Public Domain Mark 1.0 license:
https://www.rvdata.us/data.

# Event listings output by NES-LTER REST API

NES-LTER maintains a RESTful Application Programming Interface (REST
API) to provide a set of consistent URLs that, when fetched, returns
data in machine-readable form that may be used by application code. For
the events product provided by the NES-LTER REST API, a subset of
columns is retained from the original elogs, including date, time,
ship's position, instrument, and action (parsing code available at:
https://github.com/WHOIGit/nes-lter-ims/blob/master/neslter/parsing/elog.py).
For some but not all cruises we corrected and/or added events. Blanks
are retained (not filled with missing value code) in the station, cast,
and comment columns. Event logs are available per-cruise with the
following URL pattern, using cruise en627 as example:
https://nes-lter-data.whoi.edu/api/events/en627.csv.

# Data assembly

The concatenated data product is built from event logs output by the
NES-LTER REST API. In this first version of this data package, we used a
script in Python to acquire all available elogs from the REST API and
concatenate into a file "nes_lter_events_raw.csv" that is used in the
data assembly script in R (file and code available at:
https://github.com/WHOIGit/nes-lter-events-transect). In subsequent
versions of this data package, we acquire all available elogs in R using
the REST API end point, https://nes-lter-data.whoi.edu/api/events.
Cleaning of the concatenated table included formatting datetime,
excluding extraneous columns, and excluding instruments specific to
Ocean Observatories Initiative (OOI)-led cruises (CPM, CSM, Falcon ROV,
Glider, Kraken ROV, REMUS, Slocum Glider, USBL). We did not exclude
events listed with instrument "Other" that are pertinent to OOI-led
cruises. We added a column project_id to indicate LTER-dedicated or
partner cruises.

# Quality Assurance

We assured that the geographic and temporal coverage of the concatenated
data product were within expected ranges. For corrections made or still
needed for the NES-LTER REST API product, see README per-cruise with the
following URL pattern, using cruise en627 as example:
https://nes-lter-data.whoi.edu/api/events/en627/README. We did not yet
regularize the names of LTER-specific instruments, for example "Bongo"
and "Bongo net" are equivalent. For cruises prior to ar28a in spring
2018, we had not yet established controlled vocabulary terms related to
IFCB, nor had we distinguished the instrument "IFCB continuous" from
underway science seawater with action "IFCB discrete". For cruises
en608, ar28b, and ar31c, the instrument IFCB refers to IFCB continuous.
For cruises ar24a and ar24c, the instrument IFCB109 represents IFCB
continuous, and the instrument IFCB102 represents an IFCB analyzing
discrete samples.
