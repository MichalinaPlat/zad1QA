# zad1QA

Feature: authenticate to the application
  	  A regular user should be able to authenticate to the application and then he can see his account details.
   		 Rules:
     		 -	User must be registered user
     		 -	Registered user must fill login field with valid email address, up to 60 characters and with correct 				password
      
Scenario: registered user successful authenticate to the application

	  Given user is a registered user 
	  And he is on login page
	  When he fills login field with valid email address, up to 60 characters
	  And he fills correct password 
	  Then he authenticates to the application
    And he can see his account details – name, surname, email address, mailing address

Scenario Outline: registered user unsuccessful authenticate to the application 

	  Given user is a registered user 
    And his valid email: User1@app.pl, correct password: Admin123!
	  And he is on login page
	  When he fills login field with <login>
	  And he fills <password>	
	  Then he doesn’t authenticates to the application
    And he should see error message "Authentication failed. Login or password are incorrect.”
	  And he can’t see his account details 

Examples:

|login	          |password   |
|user1@app.pl	    |Admin123!  |
|User2@app.pl	    |Admin123!  |
|User1@app.p	    |Admin123!  |
|User1#app.pl	    |Admin123!  |
|User1@ap.pl	    |Admin123!  |
|User11@app.pl	  |Admin123!  |
|User1@app.com	  |Admin123!  |
|User1@wp.pl	    |Admin123!  | 
|User1@app.pl	    |Admin123   |
|User1@app.pl	    |Admin1234! |
|User1@app.pl	    |Admin123$  |
|User1@app.pl	    |Adminn123! |
|User1@app.pl	    |Admin      |
|User1@app.pl	    |admin123!  |
|User2@app.pl	    |Adin123!   |
|User1@app.p	    |Admin133!  |
|User1#app.pl	    |admin123@  |
|	                |Admin123!  |
|User1@app.pl	    |           |

Scenario: unregistered user unsuccessful authenticate to the application 

	  Given user is unregistered user
	  And he is on login page
	  When he fills login field with User1@app.pl
	  And he fills password “Admin123!”
    Then he doesn’t authenticates to the application
	  And he should see error message "Authentication failed. Login or password are incorrect.”
	  And he can’t see his account details

Scenario Outline: registered user with incorrect logon unsuccessful authenticate to the application 

	  Given user is a registered user 
    And his correct password: Admin123!
  	And he is on login page
  	When he fills login field with <login>
  	And he fills password “Admin123!”
    Then he doesn’t authenticates to the application
	  And he should see error message "Authentication failed. Login or password are incorrect.”
	  And he can’t see his account details 

Examples:

|login                                                                      |
|useruseruseruseruseruseruseruseruseruseruseruseruseruseruseruser@app.pl    |
|User111111111111111111111111111111111111111111111111111111111@app.pl       |


