# NINA-NightReport
Automated N.I.N.A session reporting: parses log files and the CSV metadata of the Session Metadata Plugin by @tcpalmer. The reporting to be send via Discord webhook. Generates optional charts.

NINA-NightReport reads your N.I.N.A logs and Plugin Session Metadata CSVs, computes the previous night’s log (sunset to sunrise) or from your selected date (end date of the session must be provided via --date cli command). 
Aggregates per-filter imaging stats, and posts a Discord embed (with an optional PNG chart). It’s designed to be fault-tolerant when for example weather data are absent.

**Features**
- Auto “last night” detection from coordinates (sunset→sunrise via PY Astral).
- Parses N.I.N.A logs (multi-line safe) and discovers plugin CSVs (Image/Weather/Target).
- Per-filter summary: exposure counts & total time; HFR, FWHM, eccentricity, guiding RMS, detected stars; stability indicators.
- Overhead calculations: autofocus runs (completed/failed + durations), dither runs, filter changes, focuser moves, warnings/errors.
- Optional PNG chart (HFR vs focuser temp, eccentricity vs guiding RMS, stars/sky quality, sky temperature).
- Discord webhook delivery (image attached if a chart is generated).

## Usage
usage: NINA-NightReport.exe [-h] [--date DATE] [--coordinates COORDINATES] [--webhook WEBHOOK] [--no-plot]

options:
  -h, --help            show this help message and exit
  
  --date DATE           Reference date for selecting the night window (YYYY-MM-DD, 'yesterday'/'today'). Interpreted
                        as the night ending at this date's sunrise. Default: last night.
  
  --coordinates COORDINATES
                        GPS coordinates as 'lat,lon' (used for sunset/-rise calculations to strip the NINA log file).
  
  --webhook WEBHOOK     Discord webhook URL (https://discord.com/api/webhooks/xxxxxxxx)
  
  --no-plot             Skip chart generation and send text-only embed.


To start the tool in the morning via External script command in the N.I.N.A Advanced Sequencer best to build a small nightreport.bat as following:

@echo off

Start 'Your Path'\NINA-NightReport-beta.exe --webhook 'your webhook'




> ⚠️ **Pre-release Notice**
>
> This project is a **pre-release** intended for testing and evaluation.
> Use at your **own risk**. The software is provided **“as is”**, **without
> warranty** of any kind. Functionality, CLI flags, and data formats may
> change without notice and may introduce **breaking changes**. Do not rely
> on this tool for critical operations; always validate results.
>
> Keep your secrets safe (e.g., webhooks/tokens).
> Feedback and preporting on issues are highly welcome.
