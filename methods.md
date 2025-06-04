# Original event logs

Events were recorded onboard with Rolling Deck to Repository (R2R) event
logger (elog) software described at:
https://www.rvdata.us/about/event-log. Prior to each cruise an NES-LTER
Information Manager works with shipboard technicians and the R2R elog
software team to configure the elog with instruments and actions from a
controlled vocabulary. The event log is started when the ship leaves
port and concluded upon arrival. During the cruise, events are added
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
NES-LTER REST API (https://github.com/WHOIGit/nes-lter-ims/wiki/Using-REST-API-to-access-NES-LTER-data). 
Event logs are concatenated and standardized in the 
data package assembly R markdown script (available at 
https://github.com/WHOIGit/nes-lter-events-transect).
Cleaning of the concatenated table included formatting datetime,
excluding extraneous columns, and excluding instruments specific to
Ocean Observatories Initiative (OOI)-led cruises (CPM, CSM, Falcon ROV,
Glider, Kraken ROV, REMUS, Slocum Glider, USBL). However,
events listed with instrument "Other" that are pertinent to OOI-led
cruises are included. We added a column project_id to indicate LTER-dedicated or
partner cruises. We standardized instrument names across all events 
to enable streamlined searching across all cruises. We also regularized 
vocabulary used for underway science seawater, including actions for 
those events.

# Quality Assurance

We assured that the geographic and temporal coverage of the concatenated
data product were within expected ranges. For corrections made or still
needed for the NES-LTER REST API product, see README per-cruise with the
following URL pattern, using cruise en627 as example:
https://nes-lter-data.whoi.edu/api/events/en627/README. 

# Differences from previous version

For version 2, instrument names were standardized, along with the vocabulary used for underway science seawater. Date-time format was updated from "YYYY-MM-DD hh:mm:ss" to "YYYY-MM-DDThh:mm:ssZ". 

Previously, a separate python script was used to acquire all available elogs from the REST API and
concatenate into a csv file that was then regularized in the 
data package assembly R markdown script. In version 2, all available elogs are concatenated in the data package assembly itself.
