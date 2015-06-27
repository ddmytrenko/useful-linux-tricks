### How to convert .mov file to .avi file?

	$ ffmpeg -i file-name.mov -g 60 -vcodec msmpeg4v2 -acodec pcm_u8 -f avi file-name.avi

### How to split ape+cue or flac+cue pair into separate mp3 tracks with the highest quality?
At first of all we have to install mac, flac, wavpack, vorbis-tools, shntool, cuetools and mp3info. Than just run something like:

	$ shnsplit -f file.cue \
	-o "cust ext=mp3 lame --quiet --alt-preset insane - %f" \
	file.ape

NOTES: "insane" prest for lame means 320 kbit/s of constant bitrate. See the link below for more information: http://goo.gl/pwxNLf .

### Fix "Could not open a connection to your authentication agent." when using `ssh-add`
If you're trying to add identities to the authentication agent using ssh-add you might get the following error:

	Could not open a connection to your authentication agent.

The reason, as the error message suggests, is that `ssh-add` doesn't know how to "talk" with the authentication agent. The problem can be solved by setting `SSH_AUTH_SOCK` environment variable. If you run `ssh-agent` you should get some output like this:

	SSH_AUTH_SOCK=/tmp/ssh-agVZL13989/agent.13989; export SSH_AUTH_SOCK;
	SSH_AGENT_PID=13990; export SSH_AGENT_PID;
	echo Agent pid 13990;

now if you evaluate the command output in your shell, the variable will be set:

	eval $(ssh-agent)

### How do you reload your .vimrc file without restarting vim?

If you are editing your vim configuration, you can reload it with:

	:so %

`%` stands for current file name (see `:h current-file`) and `:so` is a short form of `:source`, which reads the content of the specified file and treats it as Vim code. In general, to re-load the currently active `.vimrc`, use the following (see http://dailyvim.blogspot.com/2008/11/reload-vimrc.html):

	:so $MYVIMRC
