# Changelog

All notable changes to this extension are documented here. The format
is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/).

## [1.0.8] - 2026-09-29

### Removed
- Install and heartbeat reporting: `Service\InstallReporter`, `Cron\SendHeartbeat`, `Setup\RecurringData` and the `panth_notfoundpage_send_heartbeat` cron job. The module no longer contacts any external server, neither during `setup:upgrade` nor from cron.
