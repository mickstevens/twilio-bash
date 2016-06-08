How to send a Twilio SMS from the Shell

The twilio-sms bash script will send an SMS to one or more phone numbers provided on the command line, using content read from STDIN! It can practically be used as a drop-in replacement for mail in some instances.

The script can read configuration parameters, such as your Twilio AccountSid, AuthToken and CallerID from the command line, or more preferably from a config file. You can provide the path to a config file in the arguments, or the default ~/.twiliorc will be tried.

Additionally, you can provide one or more phone numbers in a single invocation of the script, and all the numbers will be texted.

Usage: twilio-sms [-v] [-c configfile] [-d callerid] [-u accountsid] [-p authtoken] number [number[number[...]]]
Installation

Download the twilio-sms bash script and put it somewhere in your path:
https://www.twilio.com/packages/labs/code/bash/twilio-sms
chmod 775 twilio-sms
Optional: Setup a default config file in ~/.twiliorc or a location of your choice

Example Usage

echo "Hi There" | ./twilio-sms 415-555-1212
Will text "Hi There" to 415-555-1212.

echo "Hi There" | ./twilio-sms 415-555-1212 415-555-1313
Will text "Hi There" to 415-555-1212 and 415-555-1313.

echo "Hi There" | ./twilio-sms -u AC12345... -p d45bd.. -d 555-867-5309 415-555-1212
Will text "Hi There" to 415-555-1212, and the SMS will come from your Twilio phone number 555-867-5309, and the AccountSid and AuthToken will be used to authenticate with Twilio's API.

echo "Hi There" | ./twilio-sms -c /etc/twilio.conf 415-555-1212
Will text "Hi There" to 415-555-1212 using AccountSid, AuthToken and CallerId parameters read from /etc/twilio.conf.

echo "Hi There" | ./twilio-sms -v 415-555-1212
Will text "Hi There" to 415-555-1212 running in verbose mode, meaning it outputs to STDOUT the XML response received from the Twilio REST API.

Config File

The config file consists of bash variable declarations, as name=value pairs, each on one line. The file may contain any of the following parameters that will be used as defaults and therefore, don't need to be specified on the command line:

Attribute Name	Description
ACCOUNTSID	Your Twilio AccountSid. For example: AC1234567890
AUTHTOKEN	Your Twilio AuthToken. For example: dk49dkdcb3948abd
CALLERID	A valid Twilio phone number configured for your account. Note: must be a phone number purchased from Twilio, a validated caller-id will not work. For example: 555-867-5309
Example Config File

ACCOUNTSID=AC1234567890
AUTHTOKEN=dk49dkdcb3948abd
CALLERID=555-867-5309
