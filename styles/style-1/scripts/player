#!/bin/sh

fetch() {
	player=$(eval "playerctl -l | head -n 1" 2>&1)
	symbol="<span>  </span>"
	name=$(eval "playerctl metadata title" 2>&1)
	artist=$(eval "playerctl metadata artist" 2>&1)
	case "$player" in
		"chromium"* )
			symbol="<span>  </span>"
			if [ -z "$artist" ]; then
				artist="via Chromium"
			fi
			return;;
		"firefox"* )
			player=$(playerctl metadata | grep url)
			case "$player" in
				*"youtube"* )
					symbol="<span>  </span>"
					return;;
				*"reddit"* )
					symbol="<span>  </span>"
					artist="via Reddit"
					return;;
				* )
					symbol="<span> 󰈹 </span>"
					if [ -z "$artist" ]; then
						artist="via Firefox"
					fi
					return;;
			esac;;
		"spotify" )
			symbol="<span>  </span>"
			return;;
	esac
}
process() {
	if [ -z "$name" ]; then
		name="Unknown media"
	fi
	if [ -z "$artist" ]; then
		artist="Unknown artist"
	fi
	if [ "$player" = "No players found" ]; then
		name="No media playing"
		artist="No media playing"
	fi
	if [ "${#name}" -gt "23" ]; then
		name="$(echo "$name" | cut -c1-20)..."
	fi
	if [ "${#artist}" -gt "23" ]; then
		artist="$(echo "$artist" | cut -c1-20)..."
	fi
	artist="<span style=\"italic\" weight=\"light\"> $artist </span>"
}

fetch
process
case "$1" in
	"-s" )
		echo "$symbol";;
	"-n" )
		echo "$name";;
	"-a" )
		echo "$artist";;
esac
