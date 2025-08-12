# NINA-NightReport
Automated N.I.N.A session reporting: parses log files and the CSV metadata of the Session Metadata Plugin by @tcpalmer. The reporting to be send via Discord webhook. Generates optional charts.


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
