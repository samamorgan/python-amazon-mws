[![slack](https://img.shields.io/badge/slack-python--amazon--mws-blue?style=for-the-badge&logo=slack)][slack_invite]
![CI Testing](https://img.shields.io/github/workflow/status/python-amazon-mws/python-amazon-mws/Testing/master?logo=github&style=for-the-badge)

# python-amazon-mws

python-amazon-mws is a Python connector to [Amazon Marketplace Web Services][2]
(or MWS). It provides a simple way to build and send requests to MWS,
allowing access to all that MWS can do from your Python application.

## ⚠️ Legacy version

![PyPI](https://img.shields.io/pypi/v/mws?logo=pypi&logoColor=ffffff&style=for-the-badge)

You are viewing a **legacy** version of python-amazon-mws, v0.8. More current versions are available in the `develop` branch of this repo.

To use the latest version (v1.0dev), please check the `develop` branch.

# Installation

Install the latest version from PyPI.

```
pip install mws
```

Currently the `mws` package on PyPI points to the 0.x branch, but at some later point may point to 1.x.

| Versions | Description                                                                                                                                                                                | Branch  |
|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|
| 0.x      | A backwards-compatible drop in replacement for the original package (i.e. same method signatures, class names, etc) with some extra features and anything that was obviously broken fixed. | master  |
| 1.x      | New features along with backwards-incompatible API changes.                                                                                                                                | develop |

If you want to continue using the 0.x versions, please pin your package to major version 0. i.e use something like `mws~=0.8.6` in your project's `requirements.txt`.

If you want to use 1.x functionality right now, you can install directly from the Git repo.

```
pip install git+https://github.com/python-amazon-mws/python-amazon-mws.git@develop#egg=mws
```

# Quickstart

Export your API credentials as environment variables in your shell.

```
export MWS_ACCOUNT_ID=...
export MWS_ACCESS_KEY=...
export MWS_SECRET_KEY=...
```

Now you can experiment with the API from within an interactive Python shell e.g.

```
>>> import mws, os
>>> orders_api = mws.Orders(
...     access_key=os.environ['MWS_ACCESS_KEY'],
...     secret_key=os.environ['MWS_SECRET_KEY'],
...     account_id=os.environ['MWS_ACCOUNT_ID'],
...     region='UK',   # defaults to 'US'
... )
>>> service_status = orders_api.get_service_status()
>>> service_status
<mws.mws.DictWrapper object at 0x1063a2160>
>>> service_status.original
'<?xml version="1.0"?>\n<GetServiceStatusResponse xmlns="https://mws.amazonservices.com/Orders/2013-09-01">\n  <GetServiceStatusResult>\n    <Status>GREEN</Status>\n    <Timestamp>2017-06-14T16:39:12.765Z</Timestamp>\n  </GetServiceStatusResult>\n  <ResponseMetadata>\n    <RequestId>affdec68-05d2-4bc5-a8a4-bb40f307dd6b</RequestId>\n  </ResponseMetadata>\n</
GetServiceStatusResponse>\n'
>>> service_status.parsed
{'value': '\n    ', 'Status': {'value': 'GREEN'}, 'Timestamp': {'value': '2017-06-14T16:39:12.765Z'}}
>>> service_status.response
<Response [200]>
```

# Development
All dependencies for working on `mws` are in `requirements.txt` and `docs/requirements.txt`.

## Tests
Tests are run with pytest. We test against all Python 3.6+ versions using GitHub Actions.

## Documentation
Docs are built using Sphinx. Change into the `docs/` directory and install any dependencies from the `requirements.txt` there.

To build HTML documentation, run:

```
make html
```
The output HTML documentation will be in `docs/build/`.

To run a live reloading server serving the HTML documentation (on port 8000 by default):

```
make livehtml
```

## Contributing
Please make pull requests to `develop`. Code coverage isn't necessary but encouraged where possible (especially for anything which might behave differently between Python 2/3).

[2]: http://docs.developer.amazonservices.com/en_US/dev_guide/index.html
[slack_invite]: https://join.slack.com/t/pythonamazonmws/shared_invite/enQtOTcwNTAzNjI4OTc2LTQyMzk1YzIxNTU0MmE1MWE0ZDUzZjBhMjI2ODZhNTQ5Mjk3ZTUyOGFkODk1N2Q2NjczZjY2M2U3NzAzNDU4ZTc
