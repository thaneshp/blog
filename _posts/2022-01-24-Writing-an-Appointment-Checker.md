---
layout: post
title: "Writing an Appointment Checker"
published: false
---

A few weeks ago, some members of my family needed to book appointments on a website concerning their identification. However, they couldn't get a spot as all appointments were booked out for the year of 2022.

Regardless, they kept accessing the website from time to time, in hopes that someone would cancel their appointment and they could swoop in. But the odds of finding an appointment randomly were low.

I thought about how this process of checking was manual, repetive and automatable. So I got to work and began figuring out a way to automate this for them.

In this post, I will discuss the approach I took, the tools/technologies I used and the possible downfalls in the hosts website.

Here is the link to the project github repository: [https://github.com/thaneshp/appointment-checker](https://github.com/thaneshp/appointment-checker)

## Initial Outlook

To begin, I thought about how a human would navigate the webpage and listed every step.

After attempting to book an appointment several times, I realised that there were fundamentally four steps of navigation:

1. Click and select a preferred location from the 1st drop-down field.

2. Click and select the reason for their appointment from the 2nd field.

3. Click on the date input field for the date selector to appear.

4. Cycle through the calendar, checking for any available dates.

<p align="left" style="margin-bottom: 3%; margin-top: 1%;">
<img style="box-shadow: 0px 0px 10px 0px rgb(0 0 0 / 50%);" src="../images/appointment-checker/website-interaction-steps.jpg" />
<br/> <i>Figure 1: Appointment Website Layout.</i>
</p >

To translate this into code, I needed to include opening/closing of the browser, appointment checking and alerting of subscribers.

<p align="left" style="margin-bottom: 3%; margin-top: 3%;">
<img style="box-shadow: 0px 0px 10px 0px rgb(0 0 0 / 50%); " src="../images/appointment-checker/flowchart.jpg" />
<br/> <i>Figure 2: Flowchart of Appointment Checking Steps</i>
</p >

## Implementation

At this stage, I had plan in mind and was ready to get stuck into the code.

### Interacting with HTML Elements

From my research, I found out that using Selenium with Python was the best way to go about this. With Selenium, you can go interact with HTML elements in Python through their `id`, `tag`, `xpath` and more.

For example, to select and pre-fill the first two input fields, I used the `id` field as shown below.

```python
location_field = driver.find_element_by_id(FIRST_SELECT_ELEMENT_ID)
Select(location_field).select_by_value(FIRST_SELECT_ELEMENT_VALUE)
```

To aid me with using this library, I downloaded the [SelectorsHub - XPath Plugin](https://chrome.google.com/webstore/detail/selectorshub-xpath-plugin/ndgimibanhlabgdgjcpbbndiehljcpfh) on Google Chrome which indicates how to select specific elements using Selenium.

### Determining an Available Date

Now that I had a way of interacting with the HTML elements, I needed to figure out how to search for and determine an available date.

The question I was dealing with was, "What makes a date available?"

From interacting with website, I realised that a date is available when it can be clicked on; but how does that look like in code?

Using the trusty inspect element, I discovered that a date is clickable when it has the `a` tag and un-clickable when it has the `span` tag. Now that I knew this, it was a matter of looping through all the dates and checking if any were 'clickable'. The moment a 'clickable' date is found, the date is recorded, the loop broken and a notification sent.

### Alerting Subscribers

Once a date was found, the script needed to inform a person to take action. 

Initially, I only added email notification; using the `smtplib` module and configured it using one of my personal Gmail accounts. This worked well, however, I noticed that subscribers couldn't respond fast enough as they weren't likely to check their emails very often.

Due to this, I added SMS notification using Twilio API. Their free-trial was all I needed for this, but it included their default text in every message sent. Regardless, their service is reliable and easy to set up.

Adding SMS increased user response times significantly as people were more likely to see the alert immediately.

### Automating Script Execution

Now that the script was ready, I needed a way of running it automatically and continously.

To do this, I used VMware Workstation on my secondary PC to deploy an Ubuntu VM. On this VM, I used `crontab` to configure this script to run every minute and log the output to a `.txt` file.

At this point, it was time to sit back and wait...

### High-Level Overview

From a high-level, this is what the implementation looks like.



<p align="left" style="margin-bottom: 3%; margin-top: 3%;">
<img style="box-shadow: 0px 0px 10px 0px rgb(0 0 0 / 50%); " src="../images/appointment-checker/high-level-implementation.jpeg" />
<br/><i>Figure 3: High Level Implementation Diagram</i>
</p >

## Areas of Improvement

This script is by no means perfect, but it does the job.

Fundamentally, I think there a few areas that it can be improved upon.

### 1. Efficient Date Checking

Right now, this script is checking every possible date on the date-picker UI. However, upon looking at their source code, it appears that many dates are permanently disabled, e.g. weekends and public holidays.

As such, parts of the script can be re-written to check dates that could potentially show up as an available option; making it more efficient.

### 2. Find <u>all</u> Available Dates 

Currently, the script will find the first available date, notify the subscibers and stop running.

However, it could be extended to continue traversing the calendar to find any other available dates that exist.

To do this, we could add found dates to an array, and send this list to the users after traversing the entire calendar. This would give users more option to select from when booking a date.

Despite this, I belive it wouldn't add much value as it was extremly rare for two seperate days to show up at any give time.

### 3. Determine available time slots

At the moment, users after receiving a notification have to visit the booking website to view the available times on a given date. This means that they have to make the effort of visiting the website before determining whether the time slot is suitable for them.

Instead of this, the script should traverse the available time slots after finding an available date and include this in the notification. For example, a complete message might look like "APPOINTMENT FOUND - 22 Jan 2022 at 10:30AM".

To do this, the script would have to click on the available date, wait for time slots to populate and traverse the list that appears. However, this could add considerable amount of time to the execution. As such, I think the trade-off might not be worth it as the time saved would be the difference between securing an appointment or not.

## Conclusion

Creating this script, helped me to understand the purposes of web scraping and realise the power of automation. Prior to this, I never understood how people went about creating bots to interact with a website.

From my understanding, website owners who do not intend to have bots scrape their site should implement prevention methods. This could be detecting no. of requests coming from a certain IP or adding a CAPTCHA. However, this is a discussion for a different blog.

Ultimately, this script helped subscribers to secure appointments within a span of a week. This was significant, as prior to this they were waiting for months and were on the verge of losing hope. To me, being able to see their face light up and breathe a sigh of relief, made it all worth it.






