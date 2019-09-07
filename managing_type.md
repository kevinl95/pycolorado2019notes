# Managing Time like a Time Lord: It's bigger on the inside
## Joe Mann, Spacecraft Operations Software manager at Spire Global
---

### Why is Time Hard
37 timezones globally
Most are an hour apart
Some are only 15, 30, and 45 minutes apart
Some use daylight savings time, some don't
Some areas in states (American Indian Nations for example) don't.
Countries change timezone and DST adherence

### Best pracitces (general)
When in doubt, use UTC
Freeze time for testing- for example, freezing time during a leap year to see how your application handles it
Use timezone aware objects (not magic numbers)
Use third party libraries- pytz, dateutil (python-dateutil), delorian, freezegun, calendar