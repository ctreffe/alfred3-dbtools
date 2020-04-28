# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).


## [Unreleased]

### Changed

* `alfred3_dbtools` now relies on `alfred3` installed from pip.

* Made two changes in order to adhere closer to the zen of Python ("There should be one-- and preferably only one --obvious way to do it.")
    + `mongotools.MongoDBConnector.connect()` and `mongotools.ExpMongoDBConnector.connect()` do not return anything anymore. They just establish a connection.

    + The only way to access a database or collection for both of these classes is now via the `db` property.
        - `mongotools.MongoDBConnector.db`
        - `mongotools.ExpMongoDBConnector.db`