# How To Deploy A Webstatic on App Engine

What you need to do:

## 1. Copy Your Project ID
Create a new Google Cloud console project or retrieve the project ID of an existing project to use. You can go to your dashboard and copy the project ID then paste it on another app.

## 2. Install GCloud SDK
Install and then initialize the Google Cloud CLI: https://cloud.google.com/sdk/docs/install. i'm using 64-bit ARM archive file. Go to cloud shell > run the following command:
  ```
  curl -O https://dl.google.com/dl/cloudsdk/channels/rapid/downloads/google-cloud-cli-427.0.0-linux-arm.tar.gz
  ```
  ```
  tar -xf google-cloud-cli-427.0.0-linux-arm.tar.gz
  ```
  ```
  ./google-cloud-sdk/install.sh
  ```
  ```
  ./google-cloud-sdk/bin/gcloud init
  ```
1. (Optional) To send anonymous usage statistics to help improve the gcloud CLI, answer Y when prompted.
2. To add the gcloud CLI to your PATH and enable command completion, answer Y when prompted.

## 3. Basic Structure Project
Please refer to the Google Cloud Documentation: https://cloud.google.com/appengine/docs/legacy/standard/python/getting-started/hosting-a-static-website#creating_a_website_to_host_on_google_app_engine or you can simply check the folder of this repository. However, you can adjust the folder but you need to change the configuration on app.yaml. Please check Google Documentation for this (I won't explain app.yaml further).

## 4. App.yaml File Configuration
Edit your app.yaml file and add the following code to the file:
````
runtime: python27
api_version: 1
threadsafe: true

handlers:
- url: /
  static_files: www/index.html
  upload: www/index.html

- url: /(.*)
  static_files: www/\1
  upload: www/(.*)
````

## 5. Create Project ID Directory and Upload Your Files on Shell Editor
Go to cloud shell > shell editor > make directory with your project ID that you have copied beforehand > upload your files (index.html, css, js, images, etc) and adjust the directory/structure project as shown in the step no. 3. 

## 6. Upload Your Files to Cloud Storage
Go to cloud storage > bucket > find a Bucket which has the same name as your Project ID > upload your images, js, css, etc there. This would be a path for your index.html so it can render the page properly. Now click your file that you've uploaded (for example an image and copy the path). The path would be look like this: https://web-services-380921.appspot.com/images/profile.jpg. Don't forget to add https at the beginning of the path.

## 7. Copy The File Path and Change It on index.html File
Index.html can't read your files (css, image, js, etc) yet. In order to read the file, you must change the path that stated in your index.html to the latest path (google cloud storage version). So paste the path like I already explained in the step 6 above to your index.html resources path. For example, I'd like to change my css path:

**Before**
````
<link rel="stylesheet" href="../www/css/style.css" />
````
**After**
````
<link rel="stylesheet" href="https://web-services-380921.appspot.com/css/style.css" />
````

## 8. Deploy App
Now it's time to deploy your app. Go to cloud shell and execute the following commands:
````
cd yourprojectid
````
````
gcloud app deploy
````
````
press Y and hit enter
````
````
gcloud app browse
````
Now visit your app and the application has been successfully deployed!

