# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/), 
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Changed

* Changed the behavior of `ExpMongoDBConnector` to correspond to the newest alfred3 version. It offers support for the two added standard mongoDB collections, that can be a part of an alfred3 experiment. That means, the correct properties to access mongoDB collections are now:

    - `.exp_col` : The main experiment collection. This is where experiment data is saved to.
    - `.unlinked_col` : The unlinked collection. This is where data is saved that can and should not be linked to a specific experiment session.
    - `.misc_col` : The miscellaneous collection. This is where additional data is stored, e.g. codebook data.

    - **Notes**: The property `.db` still works, it points to the same collection as `.exp_col` .
    - The method `.connect()` and the property `.list_of_agents` where removed.

* `MongoDBConnector` now establishes a connection directly upon initialization. That means, you don't need to call the `connect()` method manually anymore.

## v0.1.4 (Released 2020-04-28)

### Changed

* `alfred3_dbtools` now relies on `alfred3` installed from pip.

* Made two changes in order to adhere closer to the zen of Python ("There should be one-- and preferably only one --obvious way to do it.")
    - `mongotools.MongoDBConnector.connect()` and `mongotools.ExpMongoDBConnector.connect()` do not return anything anymore. They just establish a connection.

    - The only way to access a database or collection for both of these classes is now via the `db` property.
        - `mongotools.MongoDBConnector.db`
        - `mongotools.ExpMongoDBConnector.db`
