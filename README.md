# mama-assessment

#############################
INSTRUCTIONS TO RUN:
#############################
1. unzip
2. navigate to project home directory in command line/ terminal. Ie - directory that contains (.idea, .mvn, log etc folders) in unzipped folder
3. run following in command line: 
mvnw package        (may need to be "mvn package" depending on operating system)
4. in terminal/ command line change to /target folder. (.jar file should be present when doing a list/ view of all files in this directory)
5. run following in command line:
java -jar ussd-0.0.1-SNAPSHOT.jar --db-username username --db-password password
6. endpoint avaiblable at localhost:8080/api/v1/ussd

#############################
ASSUMPTIONS:
#############################
1. Everything needs to be persisted.
2. WASP handles sessionId creation and expiration - not enforcing any of checks as a result.
3. Assume WASP does very little to no error handling. All exceptions need to therefore be structured such that they can be passed back to a client. Error messages were therefore customised and in some instances combined with the message, so a customer can make an appropriate selection. It is assumed the WASP implements a degree of error handling. The inputs fields in the post message are validated with assumptions made about plausible maximum lengths.
	sessionId = 40 charachters : it is unique for each session, therefore can accomodate a very wide range
	msisdn = 18 chachters : phone numbers usually 11 or 12 characters, therefore 18 characters should be safe
	userEntry = 9 : largest number needs to accomodate is amount to be transferred. Given use case probably shouldn't be transfering more than 
			R 1 million otherwise exceeding Single Discretionary Allowance limits. Given this constraint 9 charachters should be 
			a conservative limit. Minimum transactional amount not considered given busienss requirements, but should be enforced.
4. ZAR - KWS: 6.10 is a typo and should be KES.
5. Assume that there are no fees subracted during the currency conversion as not stated, but would need to be added based on percentage supplied.
6. No authentication service added as this appears to be a marketing tool open to all customers (current and future). Depends on what greater architechture looks like, but integrating with Cognito User Pools and API gateway may be one plausible solution.
7. H2 database used as most convenient solution for demo purposes. 
