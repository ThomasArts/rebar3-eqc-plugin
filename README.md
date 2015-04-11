A rebar3 plugin to enable the execution of Erlang QuickCheck properties

## Description

This plugin provides the ability to run all of the EQC properties
defined in a project's applications with a simple rebar3 command. For
a property to be executed by the plugin it must use the `prop_*`
naming convention and be exported from the module in which it
resides. The number of times each property is executed is configurable
as shown in the Configuration and Usage sections below with the
default being 100 times. For users of the full version of EQC it is
also possible to have each property execute for a certain period of
time as opposed to a fixed number of iterations per property.

Other interesting capabilities will be added soon. Some of the
possibilities include, but are not limited to the following:

* Provide options to only run the properties from specific apps or modules.
* Provide an option to only run a particular list of properties.
* Provide a way to re-test a property using a saved counterexample.
* Add an option to just set the EQC compiler directive and then do a
normal eunit test execution.

Suggestions for other useful options or additions are welcome.

## Configuration

First, configure the plugin by adding the following to the
rebar.config file:

```
{plugins, [
    {rebar_prv_eqc, ".*", {git, "https://github.com/kellymclaughlin/rebar_prv_eqc.git", {tag, "0.0.1"}}}
]}.

```

To set the number of test executions to 500 instead of the default of
100, add the following rebar.config entry:

```
{eqc_opts, [{numtests, 500}]}.
```

To specify that each property execute for 30 seconds, use this entry instead:

```
{eqc_opts, [{testing_time, 30}]}.
```

The `numtests` and `testing_time` options are mutually exclusive. If
both are specified, the `testing_time` setting is ignored.

## Usage

Execute each property the configured number of times or for the
configured duration:

```
./rebar3 eqc
```

Override the configuration in `rebar.config` or the default and
execute each property 10 times:

```
./rebar3 eqc -n 10
```

Similarly, override the configuration in `rebar.config` or the default
and execute each property for 45 seconds:

```
./rebar3 eqc -t 45
```
