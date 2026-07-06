#!/bin/sh

status() {
	if [ "$(bluetoothctl devices Connected | wc -l)" -eq "0" ]; then
		return 1
	else
		return 2
	fi
}

name() {
	status
	stat="$?"
	case "$stat" in
		1)
			name="Disconnected";;
		2 )
			name=$(bluetoothctl devices Connected | head -n 1 | cut -d " " -f3-);;
	esac
	if [ "${#name}" -gt "12" ]; then
		name="$(echo "$name" | cut -c1-9)..."
	fi
	echo "$name"
}

case "$1" in
	"-s" )
		status
		case "$?" in
			1 )
				echo "<span>  </span>";;
			2 )
				echo "<span>  </span>";;
		esac;;
	"-n" )
		name;;
esac
