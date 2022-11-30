# ESA_ass4
CS 474 Module 4 SMS API Assignment
How to use
Clone the repository.
Navigate to the directory.
Run command : npm init
Install dependencies : npm install express express-rate-limit mongoose memory-cache jsonwebtoken --save
Install and use nodemon : npm install --save-dev nodemon
In the package.json file, add "start": ""nodemon index.js under scripts
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "nodemon index.js"
  },
In index.js replace <PASSWORD> with the password provided in the submission file
Run the file using the command : npm start
Test the API on http://localhost:3000/
API
Authentication

Request URL: /login

Response:

{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6Ikp_<DUMMY_TOKEN>_jp7ImlkIjoxLFtZSI6InRlc3RfdXNlciJ9LCasdfsdfjIGKAGFkgDFGADFgADFGLJHGdfHG"
}
Under Headers, add Authorization Key as 'Bearer <generated_token>'

Inbound

Request URL: /inbound/sms

Body Parameter:

{
	"from" : "9876543210",
	"to" : "1234567890",
	"text" : "Hello darkness my old friend"
}
Response for no authorization:

Forbidden
Response for missing parameter:

{
  “message”: “”,
  “error”: “parameter <parameter_name> is missing”
}
Response for invalid parameter:

{
  “message”: “”,
  “error”: “parameter <parameter_name> is invalid”
}
Response for any unexpected error:

{
  “message”: “”,
  “error”: “unknown failure”
}
When text STOP or STOP\n or STOP\r or STOP\r\n:

'from' and 'to' pair is cached 
Response for valid parameters:

{
  “message”: “inbound sms is ok”,
  “error”: “”,
  authData: <user data>
}
Outbound

Request URL: /outbound/sms

Body Parameter:

{
	"from" : "1234567890",
	"to" : "9876543210",
	"text" : "Hello from the other side"
}
Response for no authorization:

Forbidden
Response for missing parameter:

{
  “message”: “”,
  “error”: “parameter <parameter_name> is missing”
}
Response for invalid parameter:

{
  “message”: “”,
  “error”: “parameter <parameter_name> is invalid”
}
Response for any unexpected error:

{
  “message”: “”,
  “error”: “unknown failure”
}
Response if the pair ‘to’ and ‘from’ matches the cached pair:

{
  “message”: “”,
  “error”: “sms from <from> and to <to> blocked by STOP request”
}
Response if 50 requests limit reached in last 1 hour:

Limit reached
Response for valid parameters:

{
  “message”: “outbound sms is ok”,
  “error”: “”,
  authData: <user data>
}
