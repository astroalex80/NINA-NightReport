# NINA-NightReport
Automated N.I.N.A session reporting: parses log files and the CSV metadata of the Session Metadata Plugin by @tcpalmer. The reporting to be send via Discord webhook. Generates optional charts.

Nightly Report reads your N.I.N.A logs and Plugin Session Metadata CSVs, computes the previous night’s window (astronomical dusk→dawn, 18°) or from your selected date (end date of the session must be provided via cli), 
aggregates per-filter imaging stats, and posts a Discord embed (with an optional PNG chart). It’s designed to be fault-tolerant when for example weather data are absent.

Features
    Auto “last night” detection from coordinates (sunset→sunrise via Astral, 18° depression).
    Parses N.I.N.A logs (multi-line safe) and discovers plugin CSVs (Image/Weather/Target).
    Per-filter summary: exposure counts & total time; HFR, FWHM, eccentricity, guiding RMS, detected stars; stability indicators.
    Overheads: autofocus (completed/failed + durations), dithers, filter changes, focuser moves, warnings/errors.
    Optional PNG chart (HFR vs focuser temp, eccentricity vs guiding RMS, stars/sky quality, sky temperature).
    Discord webhook delivery (image attached if a chart is generated).

## Usage
usage: NINA-NightReport.exe [-h] [--date DATE] [--coordinates COORDINATES] [--webhook WEBHOOK] [--no-plot]

Reads last night's N.I.N.A log and metadata (requires Plugin Session Metadata by @tcpalmer). Sends a Discord embed
optionally with a PNG chart.

options:
  -h, --help            show this help message and exit
  --date DATE           Reference date for selecting the night window (YYYY-MM-DD, 'yesterday'/'today'). Interpreted
                        as the night ending at this date's sunrise. Default: last night.
  --coordinates COORDINATES
                        GPS coordinates as 'lat,lon' (used for dusk/dawn).
  --webhook WEBHOOK     Discord webhook URL
  --no-plot             Skip chart generation and send text-only embed.
