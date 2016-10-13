# xocto - utilities for Python services

This repo houses various shared utilities for Python services.

## Functionality

### Event publishing

Use `events.publish` to publish application events. These will be logged as JSON
to a logger named "events". 

Sample usage:

```python
from xocto import events

events.publish(
    event="ACCOUNT.CREATED", 
    params={
        'name': 'Barry Chuckle', 
        'quote_id': 'xyz123',
    },
    meta={
        'account_id': 'A-12312345'
    },
    account=account,  # optional
    request=request,  # optional
)
```

### Event timing

Time events using:

```python
from xocto import events

with events.Timer() as t:
    # do some things

events.publish(
    event="SOMETHING.HAPPENED",
    meta={
        "duration_in_ms": t.duration_in_ms 
    }
)
```

## Contributing

Create and activate a virtualenv then:

    $ make

Test package with:

    $ make test

and:

    $ make lint  

Release to PyPI by:

1. Bumping the version in `setup.py`

2. Updating `CHANGELOG.md`

3. Running: 

        $ make publish
