Config Spreader
===============

Config Spreader is a tool for [Spacewalk](http://spacewalk.redhat.com) to mirror configuration channels from one organisation to another.

License
-------

Config Spreader is published under the [GPL v3](http://www.gnu.org/licenses/gpl-3.0.html) License.

Setup
-----

Config Sprader is set up with config_spreader.conf which is a [ConfigSpreader](http://docs.python.org/library/configparser.html) file.

### The [main] section
The [main] section has 3 key elements:

1. The server URL

    The `url` key defines the server URL. I.e.: https://yourspacewalkserver/rpc/api

2. The prefix

    default: ""
    
    The `prefix` defines a string which is prefixed before every mirrored channel. If the prefix is "\_mirrored\_" and the channel which is mirrored is called "TestChannel" the resulting channel label is "_mirrored_TestChannel".

3. Debug

    default: false
    
    possibilities: true | false

    You may enable `debug` to get a more verbose output.

### The [orgs] section

Here you can define organisations with a valid username/password mapping. Every mapping contains an arbitrary organisation name followed by a `=` and `username, password`. 
The organisation name is arbitrary because the username/password defines the organisation in spacewalk. It is only needed for the channels. But more on that matter in the next section.
Username and password may not contain white spaces or commata.

Example:
`1 = hanspeter, Golugi70`

### The channels

A channel is defined by adding a new section ("[SectionLabel]") to the config file. The SectionLabel must be the channel label in the source organisation. Every Channel section must have 2 elements, a third one is optional:

1. The source organisation

    `src_org` has to be one of the arbitrary organisation names defined in the [orgs] section.

2. The destination organisation

    `dst_org` must be one or more of the arbitrary organisation names defined in the [orgs] section.
    
3. The optional prefix

    `prefix` allows you to define a custom prefix for this channel.

### Example configuration

	[main]
	url = https://yourspacewalkserver/rpc/api
	debug = false
	prefix = _mirrored_
	
	[orgs]
	#default org
	1 = hanspeter, Golugi70
	# some other org
	2 = archibald, Mehunu31
	# and another org
	3 = Everhard, Hofatu97
	
	[someConfigChannel]
	src_org = 1
	dst_org = 2,3
	prefix = _custom-prefix_
