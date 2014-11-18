app2text
========

REST API for App2Txt

# How It Works
Hook Mobile’s App2TXT product allows app developers to extend the reach of their app beyond their base by enabling communicate with non-users through SMS, creating opportunities to convert the user bases’ personal networks into new users. 
As part of Hook Mobile’s mission to deliver high quality traffic, App2TXT will also perform number validation to ensure that the number is valid, and SMS-enable. In addition to this, Hook Mobile will manage the opt-in/opt-out process and perform spam filter.


# How To Get Started
Please contact Hook Mobile to request for new Social Invite API account.  We will need following information for provisioning:

- Company name
- Email
- Mobile app identifier (Android Market App ID or iTunes app ID)
- Callback URL for receiving invitation message status (Optional)

We will then assign you set of credential for accessing our API as well as login credential for analytic dashboard.

The next step is to begin integrating against our simple REST-based API.  You will need to build both REST client and server 
logic integrate with your service:

- Send SMS : You are the REST client, app2text is the REST server.
- Query destination validity : You are the REST client, app2text is the REST server.
- Retrieve conversation thread : You are the REST client, app2text is the REST server.
- View Message: You are the REST client, app2text is the REST server.

# Authentication
App2Text API uses Basic authentication to authenticate API requests.  Once you are provisioned with an account, 
you will be assigned an <code>apiKey</code> and a <code>secret</code>.  You will be using both the <code>apiKey</code> and the <code>secret</code> as Basic authentication username and password.

# Send SMS
The REST method for sending SMS is accessible via following service endpoint:

Production Server: 
<pre><code>https://app2text.hookmobile.com/ws/send</code></pre>

<H3>HTTP Method</H3>
POST

<H3>Content Type</H3>
application/x-www-form-urlencoded

<H3>Form Variables</H3>
Here are the valid variables defined for this operation.  Be sure to apply appropriate URL encoding to each form variable value.

- <code>phone</code> : (required) recipient phone number.
- <code>message</code> : (required) SMS message to send to recipient.
- <code>appUserId</code> : (optional) unique identifier of the sending app user.  
- <code>senderName</code> : (optional) Sender name.
- <code>senderPhone</code> : (optional) Sender phone number.  

<H3>Response Status</H3>
Upon invoking this method, client shall receive HTTP Status Code 200, indicating server has accepted and queued the request. If Client receive HTTP Status Code 4XX, it means server did not accept the request.

<H3>Response Body</H3>
The HTTP response body shall contain data in JSON format. For successful or Status Code 200 scenario, the JSON data contains following name value pairs:

- <code>messageId</code> : Tracking identifier assigned to the submitted request.  You may use this tracking identifier to query for delivery status.

In event of unsuccessful or Status 4XX Code scenario, the JSON data contains following name value pairs:

- <code>code</code> : Error code
- <code>message</code> : Detailed error description

<H3>Examples of valid API requests using cURL utility:</H3>
In this example, the customer has been assigned <code>apiKey</code> = "myApiKey" and <code>secret</code> = "mySecret".  

<pre><code>curl --user myApikey:mySecret --data "message=Bob+this+is+Phil+sending+a+message+from+my+favorite+app&amp;phone=3012223333&amp;appUserId=someUniqueIdentifier&amp;senderName=Phil&amp;senderPhone=5553046500" "https://app2text.hookmobile.com/ws/send"</code></pre>

# Query Destination Validity
Prior to sending a message you can query the server and determine if the destination phone number is valid.

Production Server: 
<pre><code>https://app2text.hookmobile.com/ws/querynetwork/json</code></pre>

<H3>HTTP Method</H3>
GET

<H3>Content Type</H3>
application/*

<H3>Variables</H3>
Here are the valid variables defined for this operation.  Be sure to apply appropriate URL encoding to each form variable value.

- <code>phone</code> : (required) recipient phone number.
- <code>type</code> : (required) "mobile" or "fixed".

<H3>Response Status</H3>
Upon invoking this method, client shall receive HTTP Status Code 200, indicating server has accepted and queued the request. If Client receive HTTP Status Code 4XX, it means server did not accept the request.

<H3>Response Body</H3>
The HTTP response body shall contain data in JSON format. For successful or Status Code 200 scenario, the JSON data contains an array of the following name value pairs:

- <code>valid</code> : This is a boolean value to indicate whether the destination is valid or not.  True equals valid and false equals invalid.
- <code>type</code> : Destination number type, "mobile" or "fixed".


In event of unsuccessful or Status 4XX Code scenario, the JSON data contains following name value pairs:

- <code>code</code> : Error code
- <code>message</code> : Detailed error description

<H3>Examples of valid API requests using cURL utility:</H3>
In this example, the customer has been assigned <code>apiKey</code> = "myApiKey" and <code>secret</code> = "mySecret".  

<pre><code>curl --user myApikey:mySecret https://app2text.hookmobile.com/ws/querynetwork/json?type=mobile&amp;phone=5553046500</code></pre>


# Retrieve Conversation Thread
With this method you can retrieve a conversation between an app user and a single destination phone number.

Production Server: 
<pre><code>https://app2text.hookmobile.com/ws/thread</code></pre>

<H3>HTTP Method</H3>
GET

<H3>Content Type</H3>
application/x-www-form-urlencoded

<H3>Variables</H3>
Here are the valid variables defined for this operation.  Be sure to apply appropriate URL encoding to each form variable value.

- <code>phone</code> : (required) recipient phone number.
- <code>appUserId</code> : (required) unique identifier of the app user.

<H3>Response Status</H3>
Upon invoking this method, client shall receive HTTP Status Code 200, indicating server has accepted and queued the request. If Client receive HTTP Status Code 4XX, it means server did not accept the request.

<H3>Response Body</H3>
The HTTP response body shall contain data in JSON format. For successful or Status Code 200 scenario, the JSON data contains an array of the following name value pairs:

- <code>reply</code> : This is a boolean value to indicate whether the message is MO or MT.  
- <code>content</code> : Message content.
- <code>date</code> : Date of the message.


In event of unsuccessful or Status 4XX Code scenario, the JSON data contains following name value pairs:

- <code>code</code> : Error code
- <code>message</code> : Detailed error description

<H3>Examples of valid API requests using cURL utility:</H3>
In this example, the customer has been assigned <code>apiKey</code> = "myApiKey" and <code>secret</code> = "mySecret".  

<pre><code>curl --user myApikey:mySecret https://app2text.hookmobile.com/ws/thread?appUserId=someUniqueIdentifier&amp;phone=5553046500</code></pre>


# View Message
With this method you can retrieve an individual message to view via web browser.

Production Server: 
<pre><code>https://app2text.hookmobile.com/ws/sms/view/{messageId}</code></pre>

<H3>HTTP Method</H3>
GET

<H3>Content Type</H3>
text/html

<H3>Variables</H3>
Here are the valid variables defined for this operation.  Be sure to apply appropriate URL encoding to each variable value.

- <code>messageId</code> : (required) messageId of the sent message.
<H3>Note:</H3> The method determines the handset type by the user-agent in the request header and defaults to Android unless "ipod", "iphone" or "ipad" are found in the user-agent in the header.

<H3>Response Status</H3>
Upon invoking this method, client shall receive HTTP Status Code 200, indicating server has accepted and queued the request. If Client receive HTTP Status Code 4XX, it means server did not accept the request.

<H3>Response Body</H3>
The HTTP response body shall contain an html representation of the message. For successful or Status Code 200 scenario.


In event of unsuccessful or Status 4XX Code scenario, the JSON data contains following name value pairs:

- <code>code</code> : Error code
- <code>message</code> : Detailed error description

<H3>Examples of valid API requests using cURL utility:</H3>
In this example, the customer has been assigned <code>apiKey</code> = "myApiKey" and <code>secret</code> = "mySecret".  

<pre><code>curl --user myApikey:mySecret https://app2text.hookmobile.com/ws/sms/view/{messageId}</code></pre>



# Status Codes

- <code>100</code> : Permission denied 
- <code>101</code> : Invalid parameter(s) in your API call
- <code>102</code> : Missing parameter(s) in your API call
- <code>103</code> : Resource not found

- <code>123</code> : Invalid phone
- <code>124</code> : Send failed
- <code>125</code> : Not a mobile phone
- <code>126</code> : Mobile device not compatible
- <code>127</code> : User opted-out
- <code>128</code> : Duplicate invitation

