# Transcode your video to enable streaming

## Introduction

This lab gives step by step guidance to transcode your video to formats which enable to stream the video in the next lab.

Estimated Time: 45 minutes

### About Product/Technology 
Concepts
* Media Workflow Task – Smallest defined work for processing to be done at a specific point in the workflow. 
A simple Media Workflow service consists of one of each below tasks: 
  * Get the Input media (media asset that is already uploaded in OCI Object Storage)
  * Transcode – This task creates multiple renditions for the media asset provided
  * Thumbnail – Generates thumbnails for the media asset 
  * Output – Stores the output asset to OCI Object Storage 
  * Streaming – Optionally the streaming channels can be preset after the media asset master playlist is created.
  * Transcription – Optionally you can generate the transcript of the media asset.
* Media Workflow - customer-defined workflow to process media content that consist of one or more Media Workflow Tasks which defines the processing to be performed.
* Media Workflow Job - Jobs are used to "run" content through a workflow. Typically, a customer will define a handful of Media Workflows and use them to create many jobs. 
* Media Workflow Configuration – Re-usable configurations/parameters that can be used to create Media Workflow via API / CLI 
* OCI Object Storage – access to the buckets required for Media Services to read/write.


### Objectives

In this lab, you will:
* Transcode your video to format that will be standard for streaming it without CDN.
* Objective 2
* Objective 3

### Prerequisites (Optional)

This lab assumes you have:
* An Oracle account
* All previous labs successfully completed

## IAM Policy

The OCI Digital Media Service requires some of the other OCI services to function.
Identity Policies that define the level of access and access to a service. The supported verbs include, inspect, read, use & manage in the order of hierarchy access.

Two type of policies are needed to fully work on the labs for digital media services.

* Granting Group access to Digital Media Services
In your organization you may want to create groups to streamline the level of access based on the type of work.
For simplicity, we create below with any-user clause.
create new policy with below statement
![IAM 01](images/01.png)

Allow any-user to *verb* *entity* in tenancy

  ```
  allow any-user to use media-family in tenancy
  ```
  ![IAM 02](images/02.png)

The policy can be defined for users, resources (like OCI Compute or OCI Functions ) that need access to the media-family as well using dynamic groups.
You should be checking with your security team or IAM team to define more specific access. 



* Allow Digital Media Services to use other OCI services 
 The tasks in Media Flows & Media Services rely on permissions to be given for it to work. So, below are required.

    ```
      Allow service mediaservices to use object-family in compartment <<videoCompartment>>
      Allow service mediaservices to use keys in compartment <<videoCompartment>>
      Allow service mediaservices to read media-family in compartment <<videoCompartment>>
      Allow service mediaservices to manage ai-service-speech-family in compartment <<videoCompartment>>
    ```
  ![IAM 03](images/03.png)

## Task 1: Create Media Flows

Now that we have taken care of the IAM policy , we are ready to create our first Media Flow.
1. Create a bucket in the compartment and upload your video.
   Ensure the bucket is in the same compartment as the Media Services IAM policies defined.
    Else, you will face error like below while creating Media Flow.
    ![Create Bucket and Upload Video](images/06.png)

2. Select "Media Services" and then "Media Flows" from OCI Main Me](images/04.png)
   This will take you the landing page of Media Flows.
3. Create the Media Flow . Remember to choose the correct compartment where the IAM policy is defined.
  ![mediaflows 01](images/05.png)
  Now you will be presented with options to customize your Media Flow

4. The tasks are presented in user friendly manner to select the input bucket from where the videos are taken in for processing.
   ![mediaflows 02](images/07.png) You may leave the other fields in transcode task as default for now.
5.  optionally, you can enable the transcribe task and it does not require any additional inputs.
   ![mediaflows 03](images/08.png) 
6. The thumbnail task can also be left default configuration or disable the task if you don't need them in your first media flow.
7. 








		![Image alt text](images/sample1.png)

  To create a link to local file you want the reader to download, use the following format.

	> **Note:** _The filename must be in lowercase letters and CANNOT include any spaces._

  Download the [starter file](files/starter-file.sql) SQL code.

	When the file type is recognized by the browser, it will attempt to render it. So you can use the following format to force the download dialog box.

	> **Note:** _The filename must be in lowercase letters and CANNOT include any spaces._

	Download the [sample JSON code](files/sample.json?download=1).

  *IMPORTANT: do not include zip files, CSV, PDF, PSD, JAR, WAR, EAR, bin or exe files - you must have those objects stored somewhere else. We highly recommend using Oracle Cloud Object Store and creating a PAR URL instead. See [Using Pre-Authenticated Requests](https://docs.cloud.oracle.com/en-us/iaas/Content/Object/Tasks/usingpreauthenticatedrequests.htm)*

3. Sub step 2

    ![Image alt text](images/sample1.png)

4. Example with inline navigation icon ![Image alt text](images/sample2.png) click **Navigation**.

5. Example with bold **text**.

   If you add another paragraph, add 3 spaces before the line.

## Task 2: <what is the action in this step>

1. Sub step 1 - tables sample

  Use tables sparingly:

  | Column 1 | Column 2 | Column 3 |
  | --- | --- | --- |
  | 1 | Some text or a link | More text  |
  | 2 |Some text or a link | More text |
  | 3 | Some text or a link | More text |

2. You can also include bulleted lists - make sure to indent 4 spaces:

    - List item 1
    - List item 2

3. Code examples

    ```
    Adding code examples
  	Indentation is important for the code example to appear inside the step
    Multiple lines of code
  	<copy>Enclose the text you want to copy in <copy></copy>.</copy>
    ```

4. Code examples that include variables

	```
  <copy>ssh -i <ssh-key-file></copy>
  ```

## Learn More

*(optional - include links to docs, white papers, blogs, etc)*

* [URL text 1](http://docs.oracle.com)
* [URL text 2](http://docs.oracle.com)

## Acknowledgements
* **Author** - <Name, Title, Group>
* **Contributors** -  <Name, Group> -- optional
* **Last Updated By/Date** - <Name, Group, Month Year>
