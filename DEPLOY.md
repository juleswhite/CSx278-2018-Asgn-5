
## Deploying 

If you already completed Asgn 4 with an earlier version of the instructions, please go ahead and update your deployment method to this version of the instructions. You can skip any steps that you have already performed (e.g., phone number provisioning, etc.).

This guide is going to walk you through deploying your code to AWS and connecting a Twilio 
phone number to it so that you can programmatically respond to text messages. The services
that your code is going to use in the cloud are: AWS Lamba, AWS S3, AWS API Gateway, AWS
IAM, AWS Cloudformation, and Twilio programmatic SMS.

## Instructions

1. If you already have an AWS credentials file, you can skip this step.
   
   You should log directly into https://aws.amazon.com/ "Sign into the console". After signing
   in, click on "Services" in the upper left and then select "IAM". Select "Users" and then
   "Add user". Provide a username, such as your first and last name concatenated together
   (e.g., bobsmith) and then make sure and check "Programmatic Access". Click the "Attach
   existing policies directly" tab and select "Administrator Access." Create the user and
   then MAKE SURE and download the CSV file with the access credentials. 
   
   Create BOTH the .aws/config and .aws/credentials files as described here: 
   https://docs.aws.amazon.com/cli/latest/userguide/cli-config-files.html
   
   Make sure that your .aws/config file has this format:
   
   ```
   [default]
   region=us-east-1
   output=json
   ```
   
   Make sure that your .aws/credentials file has this format and is filled in with the
   credentials of the IAM user that you created:
   
   ```
   [default]
   aws_access_key_id =A....Z
   aws_secret_access_key =ABC....90
   ```
   
   Write down the FULL PATH to your .aws/credentials file.
   
2. READ CAREFULLY - the instructions vary based on OS version!

   ** OS X or Windows Professional, Enterprise, Education editions with Hyper-V: **
   
   Install Docker (https://www.docker.com/get-started) and make sure it is on your path so that you can run
   "docker -v" in a terminal and see the version printed out.
   
   
   ** Windows Home or a Windows version that doesn't support modern Docker: **
   
   Install Docker Toolbox (https://docs.docker.com/toolbox/toolbox_install_windows/)
   
   Make sure that the steps in "Verify your installation" work and that you see the same output
   listed in the instructions. *Anywhere that a Docker command is listed, you should 
   run this in the terminal created by Docker Quickstart.*
   
   
   ** ALL Versions Do This **

   Test that your Docker install is working with this command:
   
   ```
   docker run -it juleswhite/cs27x:asgn4-deployer /bin/bash
   ```
   
   You should see a bash shell prompt. Check the contents of the /project directory:
   
   ```
   root@b9e0fa6ea890:/project# ls /project
   ```
   
   The project folder should be empty.
   
   **Exit the Docker container with "exit".**
   

3. Edit the ".gitignore" file (in your project and NOT inside of the Docker container) and add the following line:

   ```
   /credentials
   ```
   
   This will ensure that your credentials don't get added to your git repo, which is
   REALLY bad.
   
4. Copy your .aws/credentials file that you created earlier to the root of your project. It should be at the top-level 
   of your project WITHOUT the ".aws" directory.

5. Create a file named "Dockerfile" (no extension) in the root of the project with the following contents:

   ```
   From juleswhite/cs27x:asgn4-with-deps
   COPY src /project/src
   COPY project.clj /project/project.clj
   COPY serverless.yml /project/serverless.yml
   COPY credentials /root/.aws/credentials
   WORKDIR /project
   RUN rm -rf /project/src/autograder
   CMD sls deploy
   ```
   
6. Test that the Dockerfile was created correctly by running:

   ```
   docker build -t asgn4 .
   ```
   
   You should see "successfully built xxxxx" as the next to last line of output.
   
   
7. Create a Twilio account and enable 2-factor auth

8. You will need to fund the account with $20 (you can fund the account after class)

   When you set up billing:

   ```
   WARNING: DO NOT ENABLE AUTO-RECHARGE ON YOUR ACCOUNT

            DO NOT ENABLE AUTO-RECHARGE ON YOUR ACCOUNT

            IF YOU DO, BAD THINGS CAN HAPPEN

            YOU HAVE BEEN WARNED
   ```

   IMPORTANT:
   -----------
   At the end of the semester, you should go and release this phone number and
   cancel your Twilio account if you are no longer going to use it.

9. Go to Twilio and buy an SMS-enabled phone number with a 615 area code (or another 
    area code of your choosing) and write down the number. You can do this after
    class if needed.
    
10. Go to Twilio settings and write down your live and test credentials under Home->Settings

11. Launch a bash shell in the Docker container that you built with this command:

    ```
    docker run -it asgn4 /bin/bash
    ```

12. From within the running container, create secure secrets for your Twilio credentials in AWS, by running these
    commands (fill-in <...>):

    ```
    sls secrets set --name twilio-prod-account-sid --text <your live sid> --region us-east-1
    sls secrets set --name twilio-prod-token --text <your live token> --region us-east-1
    sls secrets set --name twilio-test-account-sid --text <your test sid> --region us-east-1
    sls secrets set --name twilio-test-token --text <your test token> --region us-east-1
    ```

13. Verify that you did everything correctly by running this command
    in the root of the project:

    ```
    sls secrets validate
    ```

    You should see output that looks like this:

    ```
    Serverless: Targeting /..../asgnX/.serverless/asgnx.zip
    Serverless: Generating Serverless Secrets Config
    Serverless: Validating secrets
    Serverless: Secrets validated
    ```
    
    **When you are done, exit the container with "exit".**

14. To learn more about serverless secrets management, see:
    https://github.com/trek10inc/serverless-secrets

15. In your project, set BucketName in serverless.yml to "cs4278-asgnx-state-<...>"(fill <...> with your
    own name). You must choose a bucket name that is globally unique to AWS S3. If you do
    not choose a unique name, you will get the 
    "bucket already exists" error described below. **Make sure that you edit all three places
    that refer to the bucket**.

16. Set "s3/s3-keystore" on line 78 of lambda.cljs to the bucket name you set in step 12.

17. To build and deploy your code to AWS, run these commands:

    ```
    docker build -t asgn4 .
    docker run -t asgn4
    ```

    This is a one-liner for OS X / Linux:

    ```
    docker build -t asgn4 . && docker run -t asgn4
    ```

    You should see something like this print out:

    ```
    Serverless: Targeting /.../asgnX/.serverless/asgnx.zip
    Serverless: Generating Serverless Secrets Config
    Serverless: Serverless Secrets beginning packaging process
    Serverless: Writing .serverless-secrets.json
    Serverless: Validating secrets
    Serverless: Secrets validated
    Serverless: Adding environment variable placeholders for Serverless Secrets
    Serverless: Packaging service...
    Serverless: Executing "lein update-in :cljs-lambda assoc :functions '[{:name "asgnx-dev-handle-msg" :invoke asgnx.lambda/receive-message}]' -- cljs-lambda build :output /.../asgnX/.serverless/asgnx.zip :quiet"
    Serverless: Returning artifact path /.../asgnX/.serverless/asgnx.zip
    Serverless: Cleaning up .serverless-secrets.json
    Serverless: Uploading CloudFormation file to S3...
    Serverless: Uploading artifacts...
    Serverless: Validating template...
    Serverless: Updating Stack...
    Serverless: Checking Stack update progress...
    ..............
    Serverless: Stack update finished...
    Service Information
    service: asgnx
    stage: dev
    region: us-east-1
    stack: asgnx-dev
    api keys:
None
    endpoints:
GET - https://abcxyz.execute-api.us-east-1.amazonaws.com/dev/msg
POST - https://defxyz.execute-api.us-east-1.amazonaws.com/dev/msg
    functions:
handle-msg: asgnx-dev-handle-msg
    Serverless: Removing old service versions...
    ```

18. Copy the endpoint URL for POST and go to Twilio. In Twilio, select the phone number
    that you purchased and set the "Messaging" / "A message comes in" to "Webhook" and then
    paste in the URL for POST. Make sure "HTTP Post" is selected after the URL. Save the
    changes. If needed, do this after class when you fund your Twilio account.

19. You should now be able to send a text message to your Twilio phone number in order to
    interact with you application

20. Whenever you make changes to your code, you can deploy the updated code to AWS by
    running these commands again:
        
    ```
    docker build -t asgn4 .
    docker run -t asgn4
    ```

21. If you did not fund your Twilio account, you can test your deployment by opening
    the GET URL in your browser and checking if "Unknown command." message is printed. 
