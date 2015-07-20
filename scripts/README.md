# Scripts
In this directory I will collect all the cool things that people
do with spotifyd. Feel free to send a pull request if you have done
something cool that is missing.

## sc
A wrapper around `socat` or `nc` that connects to spotifyd. Both versions share the exact same
functionality but differs in how they connect to spotifyd, by unix socket or by network socket.

Put any of these in your `.profile`:
```
sc () {
	echo $@ | socat - UNIX-CONNECT:/tmp/spotifyd 2>/dev/null
}
```
or
```
sc () {
	echo $@ | nc 192.168.0.119 13337;
}
```
followed by
```
export -f sc
```
and change the location of the unix socket/the IP and port of the server.

This little shell function is required by every other script so make sure you have it
installed even though you don't plan on using it directly.

## spotifyd-dmenu
Searches the queue with dmenu and plays the selected song. Provided by
[Sævar Berg](http://www.github.com/saevarb).

## spotifyd-nowplaying
Parses `sc cur_playing` and allows for customization of the output as well
as truncation and such. Ideal for trays/bars. See file for more details.
Provided by [Sævar Berg](http://www.github.com/saevarb).

## scli
Wrapper script for `sc`, keeps reading input from user so that
you don't have to retype the `sc` command. Made by [MacGuyverism](http://www.reddit.com/user/MacGuyverism)
on reddit and modified slightly by [SimonPersson](https://github.com/SimonPersson).

## spotifyd-radio.py
This script is an implementation of the radio feature of the official client.
The playlists generated by the script comes from [echonest](http://the.echonest.com/).

When the script starts it asks wether a playlist shall be generated based on a genre or an artist.
It then goes on to ask what artist or genre to use as a seed for the playlist.

A playlist is now generated and music starts playing. The script will accept feedback at any time.
This can come as an integer from 0 to 10 where 10 is a good song and 0 is a bad one, or 
with the word skip (the song sucks, never play this song again and skip to the next one).
Either of these feedbacks get sent to the echonest servers and
gets taken into account when choosing songs in the future.

This script is not perfect. If you touch the queue or the `qprint` toggle while the script is running it will mess things up.
If you skip to many songs too fast it will fail to keep up and start from track 0 again.