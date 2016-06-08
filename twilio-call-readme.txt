How to place a Twilio Call from the Shell

The twilio-call bash script will place a phone call to one or more phone numbers provided on the command line, using content read from STDIN! It can practically be used as a drop-in replacement for mail in some instances.

The bash script leverages the Message Twimlet so no webserver is needed. It just sends a message, either a text string to <Say> or the URL of an audio file to <Play>, to the message Twimlet.

The script can read configuration parameters, such as your Twilio AccountSid, AuthToken and CallerID from the command line, or more preferably from a config file. You can provide the path to a config file in the arguments, or the default ~/.twiliorc will be tried.

Additionally, you can provide one or more phone numbers in a single invocation of the script, and all the numbers will be called.

Usage: twilio-call [-v] [-c configfile] [-d callerid] [-u accountsid] [-p authtoken] number [number[number[...]]]
Installation

Download the twilio-call bash script and put it somewhere in your path:
https://www.twilio.com/packages/labs/code/bash/twilio-call
chmod 775 twilio-call
Optional: Setup a default config file in ~/.twiliorc or a location of your choice
Example Usage

echo "Hi There" | ./twilio-call 415-555-1212
Will call 415-555-1212 and say "Hi there".

echo "Hi There" | ./twilio-call 415-555-1212 415-555-1313
Will call both 415-555-1212 and 415-555-1313 and say "Hi there" to each person.

echo "http://foo.com/music.mp3" | ./twilio-call 415-555-1212
Will call 415-555-1212 and play back the audio file at http://foo.com/music.mp3.

echo "Hi There" | ./twilio-call -u AC12345... -p d45bd.. -d 555-867-5309 415-555-1212
Will call 415-555-1212 and say "Hi there", and the call will have caller-id 555-867-5309, and the AccountSid and AuthToken will be used to authenticate with Twilio's API.

echo "Hi There" | ./twilio-call -c /etc/twilio.conf 415-555-1212
Will call 415-555-1212 and say "Hi there", using AccountSid, AuthToken and CallerId parameters read from /etc/twilio.conf.

echo "Hi There" | ./twilio-call -v 415-555-1212
Will call 415-555-1212 and say "Hi there" running in verbose mode, meaning it outputs to STDOUT the XML response received from the Twilio REST API.

Config File

The config file consists of bash variable declarations, as name=value pairs, each on one line. The file may contain any of the following parameters that will be used as defaults and therefore, don't need to be specified on the command line:

Attribute Name	Description
ACCOUNTSID	Your Twilio AccountSid. For example: AC1234567890
AUTHTOKEN	Your Twilio AuthToken. For example: dk49dkdcb3948abd
CALLERID	A valid caller-id configured for your account. For example: 555-867-5309
Example Config File

ACCOUNTSID=AC1234567890
AUTHTOKEN=dk49dkdcb3948abd
CALLERID=555-867-5309
