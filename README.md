# Alert Manager Smart Silencer

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A smart service for automatically managing alert silences in Prometheus Alert Manager based on schedule annotations.

## Features

- Automatic scheduling of alert silences based on defined time windows
- Support for multiple schedules per alert
- Prometheus metrics for monitoring
- Fully configurable through environment variables
- Rotated logging with configurable settings
- Health check endpoint
- Native integration with Prometheus Alert Manager

## Prerequisites

- Python 3.6+
- Prometheus Alert Manager
- Required Python packages (listed in `requirements.txt`)

## Installation

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/alertmanager-smart-silencer.git
cd alertmanager-smart-silencer
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Configure environment variables
```bash
export ALERTMANAGER_URL="https://your-alertmanager-url/alertmanager"
export ALERTMANAGER_AUTH="username:password"
export LOCAL_TZ="Asia/Tehran"
```

### 4. Run the service
```bash
python alertmanager_silencer.py
```

## Configuration

### Environment Variables

| Variable | Description | Default Value |
|----------|-------------|---------------|
| ALERTMANAGER_URL | Alert Manager base URL | https://pmt.seo.ir/alertmanager |
| ALERTMANAGER_AUTH | Authentication credentials (username:password) | admin:SeoPrometheus#@!123 |
| LOCAL_TZ | Local timezone for schedule calculations | Asia/Tehran |
| POLL_INTERVAL | Interval for checking alerts (seconds) | 60 |
| LOG_DIR | Directory for log files | /var/log/silencer |
| LOG_FILENAME | Name of the log file | silencer.log |
| LOG_MAX_SIZE | Maximum size of log file before rotation (bytes) | 10MB |
| LOG_BACKUP_COUNT | Number of backup log files to keep | 5 |
| LOG_LEVEL | Logging level | INFO |

## Schedule Format

Schedules are defined using alert annotations with the key `silence_schedule`. The format supports multiple lines, where each line follows the pattern:

```
HH:MM;HH:MM;DAY,DAY,...
```

Example:
```
# Silence during nights on weekdays
23:00;07:00;MON,TUE,WED,THU,FRI
# Silence during weekends
00:00;23:59;SAT,SUN
```

## Metrics

The service exposes the following Prometheus metrics at `/metrics`:

- `alertmanager_silencer_silences_created_total`: Total number of silences created
- `alertmanager_silencer_silences_deleted_total`: Total number of silences deleted
- `alertmanager_silencer_api_errors_total`: Total number of API errors encountered
- `alertmanager_silencer_active_silences`: Current number of active silences
- `alertmanager_silencer_scheduled_alerts`: Current number of alerts with silence_schedule annotation
- `alertmanager_silencer_api_request_duration_seconds`: Time spent processing API requests

## API Endpoints

- `/health`: Health check endpoint
- `/metrics`: Prometheus metrics endpoint

## Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Create a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details

## Suggested Repository Name

For the GitHub repository, I suggest naming it:

`alertmanager-smart-silencer`

This name is:
- Descriptive of the tool's purpose
- Easy to remember
- Following common GitHub naming conventions
- SEO-friendly for users looking for Alert Manager tools
