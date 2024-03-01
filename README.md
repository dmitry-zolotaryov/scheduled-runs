# An experiment in scheduling runs on a single machine.

The web interface provides a means of scheduling runs at a given time interval. This is basic CRUD interface. It also lists out performed runs.

Everything is set up on a single docker image:

- The RabbitMQ instance
- The cron job
- The web interface
- The SQLite instance

## Installing

Download and install docker https://docs.docker.com/desktop/install/mac-install/ .

## Running

Firt time:

```bash
./BUILD
./RUN
```

Subsequent runs:

```bash
./RUN
```

## V1 Goals:

- Set up basic crud operations
- Set up a cron job to run scheduled events
- Set up a scheduled event handler
- Store the scheduled runs and the runs themselves

## V2 Goals:

- Create a websocket to the server that allows real-time fetching of runs
- Connect with datadog to log events
- Deploy to "the cloud"

## Database structure

```
ScheduledRun
- id: UUID
- created_on: DATETIME
- deleted_on: DATETIME
- run_every_minutes: INT
- label: TEXT

RUN
- id: UUID
- scheduled_run_id: UUID
- scheduled_on: DATETIME
- created_on: DATETIME
```

The `scheduled_on` field of the RUN indicates when the run was scheduled to perform. The `created_on` was when it was written to the database (i.e. actually executed).

Fin.
