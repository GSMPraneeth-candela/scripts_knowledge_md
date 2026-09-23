# Android Video Streaming Test

## Overview

This script runs only on Android devices. It creates Layer-4 cross-connects (CXs), which are used to start, monitor, and end the test.

Unlike a real browser, where you go to a URL and repeatedly reload, this test goes to the URL only once and maintains the connection for the entire duration. The video itself is streamed by the LANforge app on the client Android devices, and can be reviewed in the VIDEO VIEW tab.

## Required Parameters

The script requires the following parameters: --mgr, --upstream_port, --duration, --media_source, --media_quality, --url, and --test_name.

--mgr is the IP address of the LANforge.

--upstream_port is the upstream port, i.e. the source to which the report data needs to go.

--duration is the test duration. It can be given in seconds, minutes, or hours. If the value ends with 's', it is in seconds. If it ends with 'm', it is in minutes. If it ends with 'h', it is in hours. If there is no suffix, it defaults to minutes. For example, 30s is 30 seconds, 5m is 5 minutes, 1h is 1 hour, and 5 is 5 minutes.

--media_source is the streaming protocol. Only these media sources are available: dash, smooth_streaming, hls, progressive, and rtsp.

--media_quality is the video resolution. Only these media qualities are available: 4k, 8k, 1080p, 720p, and 360p.

--url is the URL of the video stream. URLs must be used with the correct --media_source.

--test_name is the name of the test. It can be any string, but it is required by the script from the CLI.

## URL and Media Source Pairing

For HLS, use:
--url "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8" --media_source hls

For DASH, use:
--url "https://dash.akamaized.net/akamai/bbb_30fps/bbb_30fps.mpd" --media_source dash

For a DASH video stream hosted on the LANforge, use:
--url "http://<mgr>/kalki/kalki.mpd" --media_source dash

## Monitored Metrics

During the test, the script monitors rx-rate, video-format-bitrate, total-wait-time, total-urls, and total-errs from CX's.

## Reported Results

Using the monitored data, the test reports the Realtime Video Rate, Total URLs per device, Max and Min Video Rate per device, and Wait Time per device.

Total URLs and Total Errors help determine whether any device failed to stream the video. The other details help review the overall test performance.

## Supported Test Modes

The test also supports Interop (WebGUI), Robo test, Band steering, and Testhouse tests.

## Default Values

The parameters can have default values. These defaults are used unless the user specifically mentions a different value.

--mgr defaults to the IP of the testbed currently in use.

--upstream_port defaults to 1.1.eth1.

--duration defaults to 1m.

--media_source defaults to hls.

--media_quality defaults to 4k.

--url defaults to "https://test-streams.mux.dev/x36xhzz/x36xhzz.m3u8".

--test_name defaults to video_streaming_test.
