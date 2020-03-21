<p align="center">
 <img src="https://raw.githubusercontent.com/JuanmaMenendez/website-change-monitor/master/public/logo.png" alt="Website Change Monitor" width="300px">
</p>
 
 <h1 align="center"> Website Change Monitor </h1>

<h3 align="center"> A small web app written in Node.js to monitor specific changes on a web page</h3>
<br /> 

<!--- BADGES-->

<div align="center">
    <img src="https://img.shields.io/badge/-website--monitor-blue.svg" alt="Website Monitor" />   
    <a href="https://nodejs.org/en/">
        <img src="https://img.shields.io/badge/node%40latest-%3E%3D%2010-brightgreen.svg" alt="NodeJS" /></a>   
    <a href="https://GitHub.com/JuanmaMenendez/Website-Change-Monitor/graphs/commit-activity"> 
        <img src="https://img.shields.io/badge/Maintained%3F-yes-green.svg" alt="Maintenance"></a>
    <img src="https://img.shields.io/badge/contributions-welcome-orange.svg" alt="Contributions Welcome">
    <a href="https://github.com/JuanmaMenendez/Website-Change-Monitor/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-blue.svg" alt="License"></a>
</div>


## Features

*  Support any public web page

*  Track specific parts (text, markup, css class, img, etc..)

*  Custom tracking frequency (seconds, minutes, hours, days)

*  Email alert notification (with [SendGrid](https://sendgrid.com/))
 
*  Slack alert notification 

*  Daily email to confirm that the app is working

*  Front page (just to check that the system is working and to ping it if necessary (Useful for Heroku) 

<br /> 

## How it works

The App request the `urlToCheck` every `checkingFrequency` and if any of the `elementsToSearchFor` are detected, a notification is sent to your Slack channel and all the `emailsToAlert` list.

<br />

## Installation

1. Clone this repo `git clone https://github.com/JuanmaMenendez/website-change-monitor.git`

2. Inside the "website-change-monitor" folder, run the command `npm install`

3. In *server.js*, edit the *"Main configuration variables"* 
    ```
    urlToCheck = "http://urlyouwant.com/tocheck";
    elementsToSearchFor = ['Text you want to watch for', 'imageYouWantToCheckItsExistence.png'];
    checkingFrequency = 5 * 60000;  //5 minutes
    ```

4. **Slack** Integration

   4.1 Activate the [WebHooks in your WorkSpace](https://api.slack.com/incoming-webhooks) and get the corresponding 'WebHook URL'  
   
   4.2 In *server.js*, set the 'WebHook URL' in `SLACK_WEBHOOK_URL = 'https://hooks.slack.com/services/T00000000/B00000000/XXXXXXXXXXXXXXXXXXXXXXXX';`  

5. **SendGrid** Email Integration

    5.1 Create a [SendGrid Free Account](https://sendgrid.com/pricing/)
    
    5.2 Create and get an [API KEY with Full Access](https://app.sendgrid.com/settings/api_keys)
    
    5.3 In *server.js*, set the *'API KEYS'* in `SENDGRID_APY_KEY = 'AA.AAAA_AAAAAAAAAAAAA.AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA';`
     
    5.4 In *server.js*, set the sender email in the *emailFrom* variable. Code: `emailFrom = "aaa@aaa.com";`
    
      Now, to avoid falling into the "SPAM" folder there are two options:

      a) Configure SendGrid to white list your sender email.
     
      Go to [https://app.sendgrid.com/settings/mail_settings](https://app.sendgrid.com/settings/mail_settings) > *Address Whitelist* > *Edit* > Add your email address (Eg: *myemail@gmail.com*) > Switch to *ON*
       
      Note: For a less chance to fall in the SPAM folder, use an email address that you own and one of [these methods](https://sendgrid.com/blog/email-authentication-explained/) to validate it.
     
      b) Put any email address in the `emailFrom` variable and add it to the *white list* in the receiver email client.
         
    5.5 In *server.js*, set the *emailsToAlert* array. Code: `emailsToAlert = ["emailOneToSend@theAlert.com", "emailTwoToSend@theAlert.com"];` 

<br /> 

## Usage

1. `node server.js`

<br /> 

## Extras

* To update the "Working OK" email notification frequency, you can change the variable `checkingNumberBeforeWorkingOKEmail`. By default it is set to 1440 (the number of minutes a day has)


