# Cloud Computing Project

#### Intelligent Email Response System
## Overview

In this project we will make use of Python and AWS to create an intelligent data engineering portfolio website. At a high-level, the website will be hosted in a serverless manner on AWS; showcasing my data engineering, cloud computing,  python, and sql projects. 

<p align="center">
  <img src="https://github.com/Explore-AI/Pictures/blob/master/ezgif.com-gif-maker.gif?raw=true"/>
  
</p>

This project will not only showcase the skill of setting up and consuming AWS services to host a website, but will also demonstrate how to use these services in creating an intelligent Natural Language Processing (NLP) service. This NLP solution will allow us to automatically populate and send intelligent emails to interested parties based on the messages they send to our website. For example, if a potential recruiter sees a particular portfolio project on the website that interests them and contacts you regarding the said project, it is possible to set up your NLP component to pick up what the tone and key phrases are in the recruiter's message. Some smart programming techniques can then be used to automatically send a response. 

<p align="center">
  <img src="https://github.com/darlingtonmaposa/intelligent-email-repo/blob/main/assets/img/portfolio/email_intelligent_system_image.png"/>
    <br> 
    <em>Figure 1: Intelligent Email Response System Overview</em>

</p>


In **Figure 1** the solutions architecture of this project is depicted. Below follows a brief description of each module in the system:

>- [x] GitHub repo which houses all the content to complete the project. 
>
>- [x] **[AWS Lambda:](https://aws.amazon.com/lambda/)** A serverless compute instance responsible for multiple processing steps:
>      - Stores the enquiry details within an AWS DynamoDB instance for later retrieval.
>      - Forwards the enquiry contents to AWS Comprehend to help formulate an intelligent response to the site visitor.
>      - Provides logic to formulate an intelligent response based on AWS Comprehend output.
>      - Upon successful completion of these tasks, invokes AWS SES to send emails to the website enquirer.
>      
>- [x] **[AWS Amplify:](https://aws.amazon.com/amplify/)** Responsible for serving the static web content hosted in GitHub which becomes the basis of the student web page.
>
>- [x] **[Amazon DynamoDB:](https://aws.amazon.com/dynamodb/)** A NoSQL database responsible for storing enquiry details from individuals visiting the student webpage.
>
>- [x] **[Anazon SES:](https://aws.amazon.com/ses/)** A code-driven email service responsible for returning an intelligent response to webpage visitors based upon their enquiries.
>
>- [x] **[AWS API Gateway:](https://aws.amazon.com/api-gateway/)** AWS service responsible for receiving enquiry details via an API call from the student webpage, and for passing these on to the internal lambda function.
>
>- [x] **[AWS Comprehend:](https://aws.amazon.com/comprehend/)** An intelligent NLP  service capable of characterising sentiment and extracting key-phrases from the ingested text. Used to detect topics within the received webpage enquiries.

## Project Steps

  [Step 1:](#1_section_id) In the first step we will make use of GitHub, which stores all of the code needed to host our static website. 
    
  [Step 2:](#2_section_id) This step is about customising the static website to suit our needs. We will use a bootstrap template to modify the look and contents of the website to fit our preferences. 
    
  [Step 3:](#3_section_id) In the third step we will use AWS Amplify to serve our modified website. 
  
  [Step 4:](#4_section_id) This step involves the creation of an AWS DynamoDB NoSQL database. This database will be used to store website data as and when visitors send an enquiry. 
    
  [Step 5:](#5_section_id) Here we will create an IAM role that will give our AWS Lambda function (created in step 6) the required permissions to interact with AWS Comprehend, AWS SES, AWS DynamoDB and AWS API Gateway.
    
  [Step 6:](#6_section_id) In this step we set up the AWS Lambda function, a Numpy ARN layer, and an AWS API Gateway trigger:
    
   - **The AWS Lambda Function** will be used to:
        - Write data to Amazon DynamoDB;
        - Generate intelligent email responses with Amazon Comprehend, and
        - Send emails with Amazon SES.

   - **Numpy ARN:**
        - AWS Lambda runs Python on a Linux operating system. This means if we want to use popular libraries such as Numpy in our lambda function, we need to configure our Linux environment accordingly. We can do this by adding layers to our lambda function. In the case of Numpy, we will be adding the relevant layer to our Linux environment.

   - **The AWS API Gateway trigger** configures a publicly accessible HTTP API which listens for POST requests from the webpage. When a request is received, its content is parsed and used to invoke the connected lambda function.   
    
  [Step 7:](#7_section_id) In this step we will configure the Lambda function created previously to write incoming data from the website to the DynamoDB database created in step four.
    
  [Step 8:](#8_section_id) This step involves the configuration of the AWS SES service so that our pipeline can send emails automatically with the help of a Lambda function.
    
  [Step 9:](#9_section_id) In this final step we will complete the NLP portion of the project with the use of AWS Comprehend and by defining additional program logic. At a high level, AWS Comprehend will be used to extract sentiment and key phrases from a message sent from your static website. Using programming logic, we will then define several helper methods and functions which will enable the population of an automated response if the extracted key phrases and sentiment align to specific operating conditions. 


Step two in the process is where we will create our website and add our relevant data science and machine learning portfolio projects. For this step we will provide you with a baseline template which you can change freely in certain areas. 

Below follows a brief description of the files in the bootstrap template:

| Folder           | File Name                | Description      |
| ---------------- | ----------------         | ---------------- |
| Assets/mail    | contact_me.js            | Contains all the code required to send data from the filled website form through the defined endpoint to the AWS Lambda function    |
| Assets/mail    | jqBootstrapValidation.js | This JavaScript file is used to check if data entered in the contact form on the website is in the correct format. If the data is in the expected format, the script will attempt to send this to a specified URL endpoint. If the data is in an incorrect format, an error message will be displayed prompting the user to input the correct information.    |
| Assets/img     | n/a                      | This folder contains all the images used within the website.                    |
| css            | style.css                | This CSS (Cascading Style Sheets) file is responsible for controlling the style i.e. look and feel of the website    |
| js             | scripts.js               | Various scripts to increase the responsiveness and utility of the website.    |
| Project root            | index.html               | This file defines our static web page, and will be worked on when personalising the website to meet our preferences.   

Within the proposed system, a database is required that will store all the data sent from the serverless hosted website. For this project, you will be using the AWS DynamoDB NoSQL database for this purpose. 

The data sent from the website will have the following schema:

> | Variable Name    | Variable Data Type | VariableDescription |
> | ---------------- | ----------------   |  ----------------   |
> | Name             | String             |  Name of the person filling out the form on the website                   |
> |                  |                    |                     |
> | Email Address    | String             |  Email address of the person filling out the form on the website          |
> |                  |                    |                     |
> | Phone Number     | Integer            |  Phone number of the person filling out the form on the website           |
> |                  |                    |                     |
> | Message          | String             |  Message to you from the person filling out the website form              |
> |                  |                    |                     |


We will create an additional parameter called `ResponsesID`.

> | Variable Name    | Variable Data Type | VariableDescription |
> | ---------------- | ----------------   |  ----------------   |
> | ResponsesID      | Integer            | Primary key used to identify reponse instance      |

The following steps will help you set this service up within the AWS ecosystem:
  
  I. Navigate to the AWS DynamoDb service via the AWS Management Console
  
  II. On the DynamoDB `Dashboard` select `Create Table`.

  <p align="center">
  <img src="https://raw.githubusercontent.com/Explore-AI/Pictures/master/db-1.PNG" style="width:550px;"/>
    <br>
    <em>Figure 2: Create a DynamoDB table</em>
  </p>
  
  III. Give our table a relevant name, for example, `my-portfolio-data-table`. Store this name for use in later stages of the project.
  
  IV. In the `Primary Key` field insert `ResponsesID` and set the type to number.
  
  <p align="center">
  <img src="https://raw.githubusercontent.com/Explore-AI/Pictures/master/db-2.PNG" style="width:550px;"/>
    <br>
    <em>Figure 3: Create a DynamoDB table</em>
  </p>  
  
  V. Click on `Create`.
  
  VI. Select the table you just created from the side panel,  and under the `Items` tab,  click on `Create Item`.
  
  <p align="center">
  <img src="https://raw.githubusercontent.com/Explore-AI/Pictures/master/db-3.PNG" style="width:750px;"/>
    <br>
    <em>Figure 4: Add new items and their data types to created table</em>
  </p>  
  
  VII. Set an initial index by entering the number '100' in the `ResponsesID` field. (Note that this field represents a unique primary key that will be generated within the Lambda function upon its execution)
  
  VIII. Click on the `+` icon and select `insert - number`. Name this item `Cell`. Enter `0123456789` in the Value field.
  
  IX. Click on the `+` icon and select `insert - string`. Name this item `Email`. Enter `student@explore-ai.net` in the Value field.
  
  X. Click on the `+` icon and select `insert - string`. Name this item `Message`. Enter `Empty Message` in the Value field.

  XI. Click on the `+` icon and select `insert - string`. Name this item `Name`. Enter `Student` in the value field.
  
  <p align="center">
  <img src="https://raw.githubusercontent.com/Explore-AI/Pictures/master/db-4.PNG" style="width:1000px;"/>
    <br>
    <em>Figure 5: Final populated table after following steps VIII - XI.</em>
  </p>   
  
  XII. Store the table entry by clicking on `Save`.
  
  XIII. Select the created table and navigate to the `Overview` tab.
  
  XIV. Scroll down and note the Amazon Resource Name (ARN)	for the created table. *Save this for later use in the IAM policy creation steps*.
  
--- 
### 5) Create an IAM Role <a id='5_section_id'></a>
---

In step 5 you once again get the chance to show off your cloud computing skills. This project involves using *a lot* of AWS services, and as such we need a comprehensive IAM Role that will adequately govern the access and authority of the AWS Lambda function. In this project you will make use of the following services:

    - AWS Lambda
    
    - AWS API Gateway
    
    - AWS Comprehend
    
    - AWS SES
    
    - AWS DynamoDB
   
  
You therefore need an IAM role to give the Lambda function the required access to the various services that we will be using in this project. In total, you need to create four policies for this IAM Role:

 | **Policy** | **Description** |
 |------------|-------------|
 |**AWS Comprehend Policy** | Allows the Lambda function to call AWS Comprehend in order calculate a sentiment score and extract key phrases from received text entered on the website. |
 |**AWS SES Policy** | Allows the Lambda function to invoke the AWS SES service in order to send automated responses via email. |
 |**AWS Basic Lambda Execution Policy** | Grants the Lambda function permission to access AWS services and resources. |
 |**AWS DynamoDB Policy** | Gives the Lambda function write permissions in order to store data from the website to a designated (existing) AWS DynamoDB table. |                                                                          

---
### 6) Set-up the Initial AWS Lambda Function and the AWS API Gateway Trigger <a id='6_section_id'></a>
---
  
In this step you will set up the AWS API Gateway and the initial AWS Lambda function. This will be a three-part process: 


#### Part 1: Lambda Initialisation

Part 1 involves creating the AWS Lambda Function with a Python 3.7 runtime. You will also attach the IAM role created within step 5 to govern the lambda function's access control.
  
  
#### Part 2: Layer Addition

In part 2, the objective is to add an ARN  layer to the generated lambda function - one for Numpy. You need to add this layer so that you may use the Numpy library building our solution i.e. the Python code telling the lambdas function what to do. Remember these layers are `region` and `runtime` specific. Find your relevant ARN [here](https://github.com/keithrozario/Klayers).
 
#### Part 3: API Gateway Creation

The final part within step 6 is to create the AWS API Gateway and set this endpoint as your lambda's function trigger. At a high level, this gateway is responsible for interfacing between your deployed website (running from AWS Amplify) and the lambda function you have created - invoking the lambda when the gateway receives an API call (HTTP POST request sent by the webpage) and passing through its data payload to the function. This process sets off a chain of programmatic events which ultimately will generate and send your intelligent email automatically.

Your API should have the following characteristics: 
 - **API Type**: HTTP.
 - **Supported Method**: POST.
 - **Utilised Authorization**: None.
 - **[Cross-origin resource sharing (CORS)](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)**: Enabled.
 - **Detailed billing**: Disabled.

The following steps might should in your endeavour. 

 
  I. Note the `API endpoint` address under the configured trigger.
  
  II. Use this API and navigate to the `contact_me.js` file in your GitHub repo created in step 1.
  
  <p align="center">
  <img src="https://raw.githubusercontent.com/Explore-AI/Pictures/master/lam-3.PNG" style="width:500px;"/>
    <br>
    <em>Figure 6: Created API Gateway</em>
  </p> 
  
  III. Replace the existing API URL with the API endpoint.
  
  IV. Commit the changes and wait for the branch to be redeployed by AWS Amplify.
  
  
| :information_source: NOTE :information_source:                                                                                                    |
| :--------------------                                                                                                                             |
| By this point in the process the website should enable you to fill out the form with the appropriate information and, upon submission, you should receive the `Your message has been sent` notification. |
  
---
### 7) AWS Lambda Function for Writing to DynamoDB <a id='7_section_id'></a>
---

We are now at a point in the project where you can start building the actual lambda functionality. Initially we will start off with the simple task of using the AWS Lambda + API Gateway to write the data coming from the website form to the previously created DynamoDB database.

  <p align="center">
  <img src="https://raw.githubusercontent.com/Explore-AI/Pictures/master/cloud-computing-project-dynamodb.gif" />
    <br>
    <em>Figure 7: Lambda writing data from the website to DynamoDB</em>
  </p> 

| :--------------------                                                                                   |
| **Set up the lambda function to write the website POST data to DynamoDB**. To get the functionality displayed in figure 7, we need to use Python to tell our AWS Lambda function what to do and how to do it. The python code is found in the solution files. 

---
### 8) AWS Lambda Function for Sending an Email with AWS SES <a id='8_section_id'></a>
---

In this step we will setup AWS Simple Email Service (SES), to programmatically send emails when required. This is a two-part process: 

 - The first part entails the verification of email addresses for the sending and receiving of messages generated by SES. 
 
 - In the second part we configure the lambda function to send emails to specified addresses when triggered by a POST request being received by the API gateway.
   
#### Part 1: Verify your Email with Amazon SES:

When using Amazon SES for the first time, all accounts start out in sandbox mode. This is to prevent new accounts from abusing the service and sending out spam emails. In sandbox mode the following restrictions apply:

 - You can only send mail to verified email addresses and domains, or to the [Amazon SES mailbox simulator](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/send-email-simulator.html).

 - You can only send mail from verified email addresses and domains.

 - You can send a maximum of 200 messages per 24-hour period.

 - You can send a maximum of 1 message per second.
    
When your account is promoted out of the sandbox, you can send emails to any recipient, regardless of whether the recipient's address or domain is verified. However, you still have to verify all identities that you use as "From", "Source", "Sender", or "Return-Path" addresses.


| You do not have to move your account out of Sandbox Mode complete the project. However, for interest, to move out of sandbox mode you can follow [these](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/request-production-access.html) instructions. |

| :--------------------                                                                                    

#### Part 2: Programmatically send an email via Amazon SES:

Having registered the necessary email addresses, we are now ready to invoke AWS SES within our lambda function to automate the sending of email messages. 

| :--------------------                                                                                   |
| The **second task involves sending a sample email to your recipient address from your sender address, using AWS SES**. For this we use another python script to programmically do so.| 

---
### 9) AWS Lambda Function for Using Amazon Comprehend <a id='9_section_id'></a>
---

In this final step we will be building out the project's NLP functionality with the help of AWS Comprehend. The NLP functionality will enable us to extract the overwhelming sentiment (categorical variable) from a message, as well as a list of its key phrases as determined by AWS comprehend. With the sentiment information and a list of key phrases, we can build in intelligent, automated email responses into our AWS Lambda function.

The **first part** is the process description; where we go through the logic of how to use AWS comprehend to extract sentiment and key phrases. The **second part** covers the helper functions utilised; where we describe two helper functions and the main lambda function required to orchestrate an intelligent automated response. The third and **final part** is an end-to-end example; where we simulate what should be achieved once the entire AWS Lambda/AWS Comprehend/AWS SES integration is built.

#### Part 1: Process Description

At a high-level, the entire intelligent response process can be described as follow:

  1. The form is filled out on the website and sent. This form contains the following sender data:
     - `name`
     - `cellphone number`
     - `email address`, and
     - `message`.
  
  2. The data passes through the AWS API Gateway and triggers the AWS Lambda function.
  
  3. The sender data is decoded.
  
  4. The `message` is used in AWS Comprehend to extract the message sentiment and a dictionary of key phrases.
  
  5. A custom helper function finds the score and value of the most likely sentiment present in the message.
  
  6. Another helper function is used to convert the list of key phrases, generated by AWS Comprehend, to a numpy array. This array contains individual words present within the key phrase dictionary. This helper function also performs a lookup - producing a set of key phrases which match a custom list of keywords we wish to detect and reply to.  
  
  7. Having extracted the above data from the received message, the following email logic can be applied:
        
```python

if message_sentiment == 'Desired_Sentiment':
    
    if (AWS_Comprehend_Extracted_Words == Provided_List_of_Words):
        generate some personalised response based on message content
        
    else:
        generate some generic response based on message content
        
```

#### Part 2: Helper Function Descriptions

In this section we provide an overview of the helper functions required to send the intelligent, automated email responses.

**Function 1 - `find_max_sentiment(Comprehend_Sentiment_Output):`**

This function extracts and returns the highest probable sentiment from a given message.
  - Input argument:
    - Comprehend_Sentiment_Output: Sentiment dictionary generated by AWS Comprehend.
  - Outputs:
    - overall_sentiment: A string representing the most probable sentiment within the message. 
    - sentiment_score: The value of the highest probable sentiment present in the message.
  
   
**Function 2 - `key_phrase_finder(list_of_important_phrases, list_of_extracted_phrases):`**

This function attempts to find a match between the words in a key phrases dictionary produced by AWS Comprehend to a provided custom list of words. The result of the search is returned as a boolean variable.
  - Input arguments:     
    - list_of_important_phrases: A string-based list of words representing topics to be detected i.e. `['CV', 'data', 'science']`
    - list_of_extracted_phrases: An AWS Comprehend key phrases dictionary. 
  - Outputs: 
    - listing: An empty list to append the individual words present in the AWS Comprehend key phrases dictionary.
    - phrase_checker: A boolean variable representing the whether a match is discovered between the function's input lists.
            
**Function 3 - `email_response(name, email_address, critical_phrase_list, sentiment_list, sentiment_scores, list_of_extracted_phrases, AWS_Comprehend_Sentiment_Dump):`**
    
This function takes in the parsed information from the sender i.e. `name`, `email_address`, the `sentiment` and the `key phrases` output from AWS Comprehend, and a `list of critical phrases`, and uses the logic described in the 'Process Description' section to populate a email. 

  - Input arguments:     
    - name: The name of the requester.
    - email_address: The email address of the requester.
    - critical_phrase_list: A list of words that you want to match to the words in the AWS key phrases dictionary.
    - sentiment_list: A list of possible sentiments that a message could contain i.e. ['Positive', 'Negative', 'Neutral', 'Mixed'].
    - sentiment_scores: The sentiment score attached to each of the listed sentiments in the `sentiment_list` as determined by AWS Comprehend.
    - list_of_extracted_phrases: A list of the individual words present in the key phrases dictionary.
    - AWS_Comprehend_Sentiment_Dump: The sentiment summary dictionary as populated by AWS Comprehend.
  - Outputs: 
    - Text: The intelligently populated email response based on the contents of the sender's message.

The email_response method works as follow:

  1. You supply a list of words which correspond to topics which you'd like to extract/filter for within an incoming website enquiry.
  2. The supplied list of words are matched with words extracted from the AWS Comprehend key phrases dictionary. 
  3. A `boolean` response is given for each match detected across various configured keyword categories.
  4. Given the match, or potentially multiple matches, you can set up logic to start building an email response sequentially.

| :--------------------                                                                                   |
| The final task of the project requires us to use the provided functions and the AWS Comprehend/AWS Lambda code aggregated_lambda_function.py to build out the full functionality of the automated project pipeline.| 
      

# End-to-end Example

In this section we will review a basic example of how an email response is generated with the full solution architecture.

Let's say someone visiting your deployed webpage posts the following sample message using the form:

> Hi Explore Data Engineering Student,
>
> I love your website and your portfolio projects. I also had a look at your GitHub page and I am quite impressed with the quality of your work.
>
> Your medium articles also captured my attention.
>
> Could you please forward me your CV so that I can present you for a potential job at one of my clients. It is for a six month contract and I feel that your experience and skills match the job specifications perfectly.
>
> Thank you so much for your time.
> 
> Kind regards,
> 
> Charlotte Regression
> 
> Senior HR Manager, Real Analytics Resources

Running this message through our AWS Comprehend service produces [these](solution_files/Example_AWS_Comprehend_Key_Phrases_Output.txt) key phrases and [this](solution_files/Example_AWS_Comprehend_Sentiment_Output.txt) sentiment classification output.

From this output it can be seen that AWS Comprehend picked up that the message has a positive sentiment, and that it contains key phrases such as: 'your portfolio projects', 'your GitHub page', 'Your medium articles', 'a potential job', etc. We can therefore set up some logic along with our helper functions to build out our responses.

To define this logic, we start by providing some sample `string` replies that we can add to our email response if certain supplied words match the words in our AWS Comprehend key phrases dictionary. These sample replies can take the following form:

**1. Sample reply if a CV related word is matched**:

```
CV_Text = 'I see that you mentioned my C.V in your message. I am happy to forward you my C.V in response. If you have any other questions or C.V related queries please do get in touch. '
```

**2. Sample reply if a portfolio project related word is matched**

```
Project_Text = 'The projects I listed on my site only include those not running in production. I have several other projects that might interest you.'
```
**3. Sample reply if a Medium article related word is matched**

```    
Article_Text = 'In your message you mentioned my blog posts and data science articles. I have several other articles published in academic journals. Please do let me know if you are interested - I am happy to forward them to you.'
```
**4. Sample reply if the detected sentiment is negative**  

```
Negative_Text = 'I see that you are unhappy in your response. Can we please set up a session to discuss why you are not happy, be it with the website, my personal projects or anything else. \n\nLooking forward to our discussion. \n\nKind Regards, \n\nMy Name'
```

**5. Sample reply if the detected sentiment is neutral** 

```
Neutral_Text = 'Thank you for your email. Let me know if you need any additional information.\n\nKind Regards, \n\nMyName'
```

**6. Sample farewell reply** 
    
```    
Farewell_Text = 'Again, Thank you for your email.\n\nIf there is anything else I can assist you with please let me know and I will set up a meeting for us to meet in person.\n\nKind Regards, \n\nMyName'
```    
    
With sample replies now defined, we can use conditional logic and string manipulation techniques to *build* up a response.

For instance, we define a `Phrase_Matcher_Project` variable that makes use of the `key_phrase_finder` function and passes a list of words that might be project related, for example `['github', 'git', 'Git', 'GitHub', 'projects', 'portfolio', 'Portfolio']`. 

If any of these words now match the extracted keywords in the Comprehend dictionary, the value of the `Phrase_Matcher_Project` variable will be `True`. We can then use conditional logic and string manipulation to add a greeting, the project text and the farewell text to an `email_reply` variable. In the example we've presented, this `email_reply` variable will take on the following form:

> Good day Charlotte Regression,
>
> The projects I listed on my site only include those not running in production. I have several other projects that might interest you.
> 
> Again, thank you for your email.
>
> If there is anything else I can assist you with please let me know and I will set up a meeting for us to meet in person.
>
> Kind Regards, 
>
> MyName

Remember that in the example additional keywords were present such as: `CV`, `projects`, `articles`, etc. We could therefore set up a CV, Project and Article phrase checker and use the same logic as discussed above to generate an intelligent automated response. The `email_response` variable would then take on the following value for the full example:

> Good day Charlotte Regression,
> 
> I see that you mentioned my C.V in your message. I am happy to forward you my C.V in response. If you have any other questions or C.V related queries please do get in touch. 
> 
> In your message you mentioned my blog posts and data science articles. I have several other articles published in academic journals. Please do let me know if you are interested - I am happy to forward them to you
> 
> The projects I listed on my site only include those not running in production. I have several other projects that might interest you.
> 
> Again, thank you for your email.
>
> If there is anything else I can assist you with please let me know and I will set up a meeting for us to meet in person.
>
> Kind Regards, 
>
> MyName
   
| :information_source: NOTE :information_source:                                                                                                         |
| :--------------------                                                                                                     
