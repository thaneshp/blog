---
layout: post
title: Deploying Your Jekyll Site on AWS
published: true
---
When I was looking to deploy my this blog on AWS, I remember searching tirelessly for a tutorial that matched my needs. After reading many articles, I managed to piece together the steps and get it working. 

In this tutorial, I will show you how you can deploy your Jekyll site (or any other static site) on AWS using S3, CloudFront and Route53. Before you get started, this tutorial assumes you already have an AWS account, a Jekyll site and a purchased domain.

# Step 1

## Creating an S3 Bucket 

The first thing you need to do is head into the AWS console, sign-in and click into S3. You should see a page like below, minus the buckets.

![step-1-s3](../images/s3-page.png)

Click on 'Create bucket' in the top right hand corner and name your bucket the same as your domain, making sure to choose the region closest to you. Under 'Block Public Access settings for bucket', untick the first checkbox to make this bucket public. You screen should be similar to below.

![step-1-s3-create](../images/s3-create.png)

Leave the rest of the settings as is and click 'Create Bucket'.

# Step 2 

## Changing the Bucket Policy

Once you've created the S3 Bucket, you'll need to change the bucket policy to provide access to the objects stored in your bucket. 

Navigate to your bucket and click on the 'Permissions' tab. Scroll down to 'Bucket Policy' and click edit. Copy & paste the json code shown below; replacing 'blog.thanesh.io' with your bucket name.

```json 
{
 "Version": "2012-10-17",
 "Statement": [
  {
   "Sid": "AddPerm",
   "Effect": "Allow",
   "Principal": "*",
   "Action": "s3:GetObject",
   "Resource": "arn:aws:s3:::blog.thanesh.io/*"
  }
 ]
}
```

# Step 3 

## Enable Static Hosting

Next, head into the 'Properties' tab and scroll down until you find 'Static website hosting'. Click the 'Edit' button on the top right hand corner and you should be directed to a settings page. 

On here, click on Enable and specify the index document of your website. You don't have to change any other settings.

![s3-static-hosting](../images/s3-static-hosting.png)

# Step 4

## Deploying Your Website

Now it's time to upload your site files into the AWS bucket you created earlier. Just before we do that, we have to do a few things to prepare our Jekyll site.

Open up your repository in your favourtie IDE and locate the _config.yml file. In here, change the url to your domain name and the baseurl to an empty string. Refer to the screenshot below.

![config-yml](../images/config-yml.png)

After you've changed this, open up your terminal, navigate to the folder of your Jekyll site and create a production build using the command below.

```bash
$ bundle exec jekyll build
```

Once this command has run successfully, you will see a new folder in your repository called '_site'. Upload the contents of this folder into your S3 bucket by drag and drop or through the 'Upload' button.

At this point, your site is live. Head into the properties tab, scroll to the bottom and click on the link shown in the 'Static Website Hosting' box. If everything has gone well, you should see your site.

![live-link](../images/live-link.png)

# Step 5

## Enabling CloudFront

Now it's time to set up CloudFront for your website. Head into the CloudFront service and click on 'Create Distribution'. You should see a form page like below.

In this page, it is very important you enter the 'Origin Domain Name' as the name you get from the endpoint. For example, the link generated for my bucket is http://blog.thanesh.io.s3-website-ap-southeast-2.amazonaws.com/. Therefore the value I will enter in this field will be blog.thanesh.io.s3-website-ap-southeast-2.amazonaws.com. Please do not select from the options given, otherwise, this will not work.

![create-distribution](../images/create-distribution.png)

You can keep most of the settings as default. Under 'Alternate Domain Names', enter your registered domain name. Next scroll to the bottom and hit "Create Distribution'. This will take about 10-15 minutes.

# Step 6 

## Linking up your Domain

At this point, we've got your website deployed and set up with CloudFront. In this final step, we want your website to point to your registered domain.

Head into Route53 and click on 'Create hosted zone'. Once you've done this, you should see a NS record in your hosted zone. Copy each of the values in this record and enter it into your domain provider. AWS will handle the configuration of the domain.

Next, while in your hosted zone, click on 'Create Record'. Here we want to connect our domain with our CloudFront distribution we created earlier. Make sure it is an 'A record' and click on the 'Alias' switch in the right hand corner. In the dropdown that appears, select 'Alias to CloudFront distribution' which prefills the region to 'US East (N. Virginia). Click into the search box and select the CloudFront distribution. 

![record](../images/record.png)

Hit 'Create Record' and you're all set! Be patient as it may take some time to set in but when you visit your domain you should see your live site.

# Step 7

## Redirection for WWW

At this point your site should be up and live. However, if you type in www before your domain, it will produce an error. 

It’s pretty much similar to whole process we’ve just done, with a few minor adjustments. When creating a bucket, you’ll want to prepend it with ‘www’ and when clicking on the ‘Static Website Hosting’ tab, you’ll want to choose the ‘Redirect’ option and set the redirection to yourdomainname.com.

Once this is done, setup a separate Cloudfront distribution that links to your ‘www’ bucket. Next, add another ‘A’ Record in Route 53 and set the Alias Target to your new Cloudfront URL and boom, you’re done! If you type www.yourdomainname.com it should redirect to yourdomainname.com.

# That's It!

Well Done! Your site is up and live. I'm sure there's other ways to publish your site but this is what worked for me. If you have any questions or are facing any problems, please do not hesitate to reach out to me.

# Contact

You can find me on any of the following places!
- Website: [https://thanesh.io/]()
- Email: [thanesh.pannirselvam@gmail.com]()
- LinkedIn: [linkedin.com/in/thanesh-pannirselvam](https://linkedin.com/in/thanesh-pannirselvam)
