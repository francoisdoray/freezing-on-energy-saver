# Freezing on Energy Saver

## Overview

When Energy Saver is active, Chrome will freeze a "browsing context group" that
has been hidden and silent for >5 minutes if any subgroup of same-origin frames
within it exceeds a CPU usage threshold, unless it: 

- Provides audio- or video-conferencing functionality (detected via microphone,
  camera or screen/window/tab capture or an RTCPeerConnection with an 'open'
  RTCDataChannel or a 'live' MediaStreamTrack).
- Controls an external device (detected via usage of Web USB, Web Bluetooth, Web
  HID or Web Serial).
- Holds a Web Lock or an IndexedDB connection that blocks a version update or a
  transaction on a different connection.
- Is opted-out via an origin trial (see below).

Freezing consists of pausing execution. It is formally defined in the Page
Lifecycle API.

The CPU usage threshold will be calibrated to freeze approximately 10% of
background tabs when Energy Saver is active.

## Motivation

When users activate "Energy Saver", they expect the browser to adapt its
behavior to maximize battery life. Tab freezing on Energy Saver helps meet that
expectation by preventing background tabs that aren't actively used from
consuming CPU excessively.

## Origin trial opt-out

A page can be opted-out from freezing by registering for the
BackgroundPageFreezeOptOut origin trial. This origin trial will be available for
a limited time, while other solution to opt-out from freezing are being
developed (see for example the [Progress Notification API](https://github.com/explainers-by-googlers/progress-notification)).

The origin trial is supported on Dev 134.0.6948.0+ or Beta 133.0.6943.17+.