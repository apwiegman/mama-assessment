# mama-assessment

# INSTRUCTIONS TO RUN:
- unzip
- navigate to project home directory in command line/ terminal. Ie - directory that contains (.idea, .mvn, log etc folders) in unzipped folder
- run following in command line: 
mvnw package        (may need to be "mvn package" depending on operating system)
- in terminal/ command line change to /target folder. (.jar file should be present when doing a list/ view of all files in this directory)
- run following in command line:
java -jar ussd-0.0.1-SNAPSHOT.jar --db-username username --db-password password
- endpoint avaiblable at localhost:8080/api/v1/ussd

# ASSUMPTIONS:
- Everything needs to be persisted.
- WASP handles sessionId creation and expiration - not enforcing any of checks as a result.
- Assume WASP does very little to no error handling. All exceptions need to therefore be structured such that they can be passed back to a client. Error messages were therefore customised and in some instances combined with the message, so a customer can make an appropriate selection. It is assumed the WASP implements a degree of error handling. The inputs fields in the post message are validated with assumptions made about plausible maximum lengths.
	- sessionId = 40 charachters : it is unique for each session, therefore can accomodate a very wide range
	- msisdn = 18 chachters : phone numbers usually 11 or 12 characters, therefore 18 characters should be safe
	- userEntry : not restricted, but validation is handled in the adapter and not in mapper. Given use case probably should not be transfering more than  R 1 million otherwise exceeding Single Discretionary Allowance limits. This constraint will serve to limit the number of charachters. 
- ZAR - KWS: 6.10 is a typo and should be KES.
- Assume that there are no fees subracted during the currency conversion as not stated, but would need to be added based on percentage supplied.
- No authentication service added as this appears to be a marketing tool open to all customers (current and future). Depends on what greater architechture looks like, but integrating with Cognito User Pools and API gateway may be one plausible solution.
- H2 database used as most convenient solution for demo purposes. 
