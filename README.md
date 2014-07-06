stratum-mining-proxy
====================

Application providing bridge between old HTTP/getwork protocol and Stratum mining protocol
as described here: http://mining.bitcoin.cz/stratum-mining.

Installation on Windows
-----------------------

1. Download official Windows binaries (EXE) from https://mining.bitcoin.cz/media/download/mining_proxy.exe
2. Open downloaded file. It will open console window. Using default settings, proxy connects to Slush's pool interface
3. If you want to connect to another pool or change other proxy settings, type "mining_proxy.exe --help" in console window.

Installation on Linux
---------------------

1. Download TGZ file from https://github.com/slush0/stratum-mining-proxy/tarball/master
2. Unpack it by typing "tar xf slush0-stratum-mining_proxy*.tar.gz"
3. Most likely you already have Python respectively OpenSSL installed on your system. Otherwise install it by "sudo apt-get install python-dev libssl-dev"
(on Ubuntu and Debian).
3. Type "sudo python setup.py install" in the unpacked directory.
4. You can start the proxy by typing "./mining_proxy.py" in the terminal window. Using default settings,
proxy connects to Slush's pool interface.
5. If you want to connect to another pool or change other proxy settings, type "mining_proxy.py --help".

Installation on Mac
-------------------
1. Download TGZ file from https://github.com/slush0/stratum-mining-proxy/tarball/master
2. Unpack it by typing "tar xf slush0-stratum-mining-proxy*.tar.gz"
3. On Mac OS X you already have Python installed on your system, but you lack the llvm-gcc-4.2 binary required to run the setup.py file, so:
3. a) If you don't want to install Xcode, get gcc here: https://github.com/kennethreitz/osx-gcc-installer
3. b) OR download Xcode (free) from the App Store, Open it up (it's in your applications folder) and go to preferences, to the downloads section and download/install the 'command line tools'. This will install llvm-gc-4.2.
4. Type "sudo python setup.py install" in the unpacked directory from step 2.
5. You can start the proxy by typing "./mining_proxy.py" in the terminal window. Using default settings, proxy connects to Slush's pool interface.
6. If you want to connect to another pool or change other proxy settings, type "mining_proxy.py --help".

N.B. Once Apple releases Xcode 4.7 they will remove the optional install of gcc (they want you to use clang). When that happens you can either choose not to upgrade, or return to the aforementioned https://github.com/kennethreitz/osx-gcc-installer and download the specific gcc binary for your version of Mac OS.

Installation on Linux using Git
-------------------------------
This is advanced option for experienced users, but give you the easiest way for updating the proxy.

1. git clone git://github.com/slush0/stratum-mining-proxy.git
2. cd stratum-mining-proxy
3. sudo apt-get install python-dev # Development package of Python are necessary
4. sudo python distribute_setup.py # This will upgrade setuptools package
5. sudo python setup.py develop # This will install required dependencies (namely Twisted and Stratum libraries),
but don't install the package into the system.
6. You can start the proxy by typing "./mining_proxy.py" in the terminal window. Using default settings,
proxy connects to Slush's pool interface.
7. If you want to connect to another pool or change other proxy settings, type "./mining_proxy.py --help".
8. If you want to update the proxy, type "git pull" in the package directory.

Compiling midstate C extension
------------------------------
For some really big operations using getwork interface of this proxy, you'll find
useful "midstatec" C extension, which significantly speeds up midstate calculations
(yes, plain python implementation is *so* slow). For enabling this extension,
just type "make" in midstatec directory. Proxy will auto-detect compiled extension
on next startup.

Usage
-------------

usage: mining_proxy.py [-h] [-o HOST] [-p PORT] [-sh STRATUM_HOST]
                       [-sp STRATUM_PORT] [-oh GETWORK_HOST]
                       [-gp GETWORK_PORT] [-nm] [-rt] [-cl CUSTOM_LP]
                       [-cs CUSTOM_STRATUM] [-cu CUSTOM_USER]
                       [-cp CUSTOM_PASSWORD] [--old-target]
                       [--blocknotify BLOCKNOTIFY_CMD] [--socks PROXY] [--tor]
                       [-t] [-v] [-q] [-i PID_FILE] [-l LOG_FILE] [-st]

This proxy allows you to run getwork-based miners against Stratum mining pool.

optional arguments:
  -h, --help            show this help message and exit
  -o HOST, --host HOST  Hostname of Stratum mining pool
  -p PORT, --port PORT  Port of Stratum mining pool
  -sh STRATUM_HOST, --stratum-host STRATUM_HOST
                        On which network interface listen for stratum miners.
                        Use "localhost" for listening on internal IP only.
  -sp STRATUM_PORT, --stratum-port STRATUM_PORT
                        Port on which port listen for stratum miners.
  -oh GETWORK_HOST, --getwork-host GETWORK_HOST
                        On which network interface listen for getwork miners.
                        Use "localhost" for listening on internal IP only.
  -gp GETWORK_PORT, --getwork-port GETWORK_PORT
                        Port on which port listen for getwork miners. Use
                        another port if you have bitcoind RPC running on this
                        machine already.
  -nm, --no-midstate    Don't compute midstate for getwork. This has
                        outstanding performance boost, but some old miners
                        like Diablo don't work without midstate.
  -rt, --real-target    Propagate >diff1 target to getwork miners. Some miners
                        work incorrectly with higher difficulty.
  -cl CUSTOM_LP, --custom-lp CUSTOM_LP
                        Override URL provided in X-Long-Polling header
  -cs CUSTOM_STRATUM, --custom-stratum CUSTOM_STRATUM
                        Override URL provided in X-Stratum header
  -cu CUSTOM_USER, --custom-user CUSTOM_USER
                        Use this username for submitting shares
  -cp CUSTOM_PASSWORD, --custom-password CUSTOM_PASSWORD
                        Use this password for submitting shares
  --old-target          Provides backward compatible targets for some
                        deprecated getwork miners.
  --blocknotify BLOCKNOTIFY_CMD
                        Execute command when the best block changes (%s in
                        BLOCKNOTIFY_CMD is replaced by block hash)
  --socks PROXY         Use socks5 proxy for upstream Stratum connection,
                        specify as host:port
  --tor                 Configure proxy to mine over Tor (requires Tor running
                        on local machine)
  -t, --test            Run performance test on startup
  -v, --verbose         Enable low-level debugging messages
  -q, --quiet           Make output more quiet
  -i PID_FILE, --pid-file PID_FILE
                        Store process pid to the file
  -l LOG_FILE, --log-file LOG_FILE
                        Log to specified file
  -st, --scrypt-target  Calculate targets for scrypt algorithm


Contact
-------

This proxy is provided by Slush's mining pool at http://mining.bitcoin.cz. You can contact the author
by email slush(at)satoshilabs.com.

Donation
--------
This project helps thousands of miners to improve their mining experience and optimize bandwidth of large
mining operations. Now it is listed on tip4commit service, so if you find this tool handy, feel free
to throw few satoshis to the basket :-).

[![tip for next commit](http://tip4commit.com/projects/322.svg)](http://tip4commit.com/projects/322)
