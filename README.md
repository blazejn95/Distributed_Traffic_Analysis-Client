The cllient part of project which sends the data(TCPDUMP files *.pcap) to server via socket. The script is designed for devices that are able to use Linux operating system such as RaspberryPi etc. On launch the client script launches another one - init.py which is responsible for starting Tcpdump in background. The process of sending files is kind of based on round robin the init.py file specifies the settings of Tcpdump thats going to run. The example settings that are currently in there are:
tcpdump -w data -i br0 -C 5 -W 2 -s 96
- -w data - name of files that are going to be written
- -i br0 - interface on which we listen 
- -C 5 - maximum file size in Mbs 
- -W 2 - number of files after which Tcpdump is going to overwrite existing files (basically cycle length, the round robin analogy)
- -s 96 - trimming the packets to 96 bytes, that way we dont need to deal with a lot of data since all the information we need for creating packet distributions etc. are included in header. Remove this part if you want the full packet length included for spying on somebody or whatever reason.
After init.py finishes his job awaiting for new files and sending them begins.
