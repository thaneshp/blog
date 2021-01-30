---
layout: post
title: Setting up AWS LocalStack
published: true
---
LocalStack is an extremely useful tool if you want to save money and avoid signing into AWS console as much as possible.

Using LocalStack gives you the ability to spin up cloud services directly on your local machine, making it more convenient to develop for the cloud.

I recently discovered LocalStack whilst working on the [Scrumblr-Enhacement project](https://github.com/zainafzal88/scrumblr-enhancement) alongside a team of members from the Dev(){CoP} community. Zain Afzal, our project lead, recommended we use LocalStack in order to simplify development and save cost. 

In this blog, I will show you how to setup LocalStack on your machine, step-by-step.

# Step 1

## Install and Run Docker

Visit https://hub.docker.com/search?q=&type=edition&offering=community. 

Search for the Docker download matching your OS and install it accordingly.

Once you have Docker installed, make sure run the application. If you've installed and run it correctly, you should see the whale icon appear on your tool bar above.

![step-1-localstack](../images/step-1-localstack.png)

All you have to do is keep it running and proceed to the next step.

# Step 2 

Visit the LocalStack repository on github via
https://github.com/localstack/localstack.

On here, locate a file called 'docker-compose.yaml' and click to open it. You should a page like below. Highlight all the text shown in this file and copy it to your clipboard.

![step-2-localstack](../images/step-2-localstack.png)

# Step 3

If you are already know what project you'll be using LocalStack for, open up that repository on your favourite IDE. Otherwise, create a test folder anywhere on your machine and open that up instead. 

For this tutorial, I will create a folder called 'localstack' on my desktop.

Once you have opened up your IDE with your chosen folder, create a new file in the repository called 'docker-composer.yaml'

![step-3-localstack](../images/step-3-localstack.png)

After you've created this file, paste the text you copied earlier and hit save.

# Step 4

Now add the AWS services you plan to use by editing the 'SERVICES' line in the 'docker-compose.yaml' file. As you can see from the image below, I have added s3, lambda and ec2.

![step-4-localstack](../images/step-4-localstack.png)

# Step 5

Open up terminal; either your IDE or directly on your machine and locate to the directory where you have your 'docker-compose.yaml' file placed.

Once you've done this, type in the following command.
```console
$ docker-compose up
```
You should see a sequence of lines show up in your terminal just like the image shown below. As you can see, the mock services we listed earlier is now running. 

![step-5-localstack](../images/step-5-localstack.png)

# Step 6
Visit https://0.0.0.0:4566 in your browser and you should see a "running" status like below.

![step-6-localstack](../images/step-6-localstack.png)

Add /health to the end of the previous url and you will see the statuses of each of the services you listed earlier. 

![step-6(2)-localstack](../images/step-6(2)-localstack.png)

# That's It!

You should be all set up and ready to start developing for AWS, locally! Hope this helped. If you have any questions or are facing any problems, please do not hesitate to reach out to me. 

# Contact

You can find me on any of the following places!
- Website: https://thanesh.io/
- Email: thanesh.pannirselvam@gmail.com
- LinkedIn: linkedin.com/in/thanesh-pannirselvam
