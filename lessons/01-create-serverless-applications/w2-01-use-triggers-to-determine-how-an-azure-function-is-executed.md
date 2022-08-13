# Use triggers to determine how an Azure Function is executed

## The best trigger for azure function

- ``Timer``
- ``HTTP``
- ``Blob``
- Queue
- Azure CosmosDB
- Event Hub

## Run an azure function a schedule

that use CRON Expression

execute every 5 min

```cron
0 */5 * * * *
```

What is the correct order for the time fields in a CRON expression?

- Seconds, minutes, hour, day, month, weekday of the week
  - The correct sequence of a CRON expression is Seconds, minutes, hour, day, month, weekday of the week.

can create at azure portal and on program at VScode, Visual studio , others
