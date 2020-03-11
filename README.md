Icinga Check Re-scheduler
=========================

A small tool to help re-scheduling a bunch of checks over a a period of time.

This is helpful when checks are scheduled too close together, especially for checks that
 
* have long execution times, or produce load
* wide check intervals
* problems caused in scheduling by check_period and high check_interval

It was written for certificate checks that should run every X hours, but were configured with a check_period of
"daytime". This caused all checks to be started in the morning when check_period began.

The following actions were taken:

* Remove check_period settings
* Re-schedule checks with this script

## Usage

Here is a brief example to re-distribute checks over the next 12 hours (720 minutes).

```
./icinga-reschedule.py \
    --ido-host mysql-server \
    --ido-database icinga2 \
    --ido-username icinga2 \
    --ido-password secret \
    --period 720 \
    --command-pipe /run/icinga2/cmd/icinga2.cmd \
    --filter-service CERT_CHECKS%
```

Please make sure to check: `./icinga-reschedule.py --help`

## Dependencies

It should run with Python 2.7 and higher, with external packages:

* [mysql-connector-python](https://pypi.org/project/mysql-connector-python/)

On CentOS / RHEL 7 with [EPEL](https://fedoraproject.org/wiki/EPEL):

```
yum install mysql-connector-python
```

## Limitations

* Only build for IDO as data source
* Only for the legacy command pipe

Both could be also done via the REST API of Icinga 2.

## License

Copyright (C) 2020 [NETWAYS GmbH](mailto:info@netways.de)

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation; either version 2 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License along
with this program; if not, write to the Free Software Foundation, Inc.,
51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.
