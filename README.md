<img src="http://wallet.crypdex.io/static/img/full-logo.svg" width=250 style="margin-bottom:0px;" />

**Come back shortly, this repo is under development**

# Flows

A curated collection of Flows for the Crypdex platform.

#### Table of Contects

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Introduction](#introduction)
- [Authoring](#authoring)
  - [Trigger](#trigger)
  - [Actions](#actions)
  - [Schedule](#schedule)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Introduction

A Flow is a tiny program that directs the Crypdex platform how to perform your cryptocurrency swap. When submitted to Crypdex, each Flow is bound to a persistent, asset address.

**Simple Authoring:** Flows are written in YAML and registered with Crypdex through an API call or at the command line using the Crypdex CLI.



## Authoring

Flows have 3 primary sections:

- **Trigger**
- **Actions**
- **Schedule** (optional)

Flows can be authored in YAML or JSON (coming soon)

```yaml
trigger: 'balance > 10'
action:
  - swap:
      target: GUSD
      address: 0x23b9320d0f0D57bdF32000083aA602e3E6c15cff
      limit: 164.12
```

### Trigger

A trigger defines the conditions that start the actions as described in the Flows contract. Only a single trigger per Flows contract is currently allowed.

The following trigger statments are supported

- `balance [>,>=,<,<=,==] [float]`

### Actions

An action block defines what to do upon the satisfaction of the condition defined in the trigger.

The action block is an array of actions, since may things can result from a trigger. All action params are required unless otherwise noted.

The following actions are supported

- `swap`
  - `target [asset]` - The target code of the asset to swap for.
  - `address [string]` - The account address of the target asset. You must control this address.
  - `limit [float] (optional)` - The lower price limit acceptable for the swap
  - `amount [float] (optional)` - The amount of target asset to fill

### Schedule

(in development)

An optional `schedule` block can be defined. This block allows SmartSwaps to be executed recurrently or over a time period.

The following keywords are supported for schedule:

- `duration [string]` - A natural language declaration of duration: i.e. "1 day", "30 seconds"
- `start [yyyy-mm-ddThh:mm:ss+|-hh:mm]` - ISO 8601 formatted date-time. If timezone is omitted, UTC is used.
- `end [yyyy-mm-ddThh:mm:ss+|-hh:mm]` - ISO 8601 formatted date-time. If timezone is omitted, UTC is used.
- `recurrence` - Accepted values: minute, hour, day, month
