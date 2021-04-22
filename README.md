# node-react
helping commands for node and react

### create node server
1. create package.json
2. ceate index.js
3. run ```npm start```


### Create React App
1. ```npm install -g create-react-app```
2. ```create-react-app app_name```
3. ```cd app_name```
4. ```npm start```
5. ```npm test```
6. npm run build (optional to run get build for react app)
7. write Dockerfile 
8. write docker-compose.yml file (docker volumes if you need runtime editing)


### Ways to Run Tests
1. Build docker image then run cmd ```docker run image-name -it npm run test```
2. for docker-compose firstly up containers then run cmd ```docker exec -it image-name npm run test```

> **_NOTE:_** To run tests automatically add command ```npm run test``` at last of service 

## Production Envoirnment
1. Added Multi-Step Dockerfile.prod with nginx
2. To build image cmd ```docker build -f Dockerfile.prod . ```
3. To run container cmd ``` docker run -p 80:80 --name node_app prod_frontend ```

![image](https://user-images.githubusercontent.com/78042886/115704070-5448cd80-a384-11eb-92b8-9bd808229245.png)


## Travis Ci
1. Create account and follow steps to attach github repo with travis-ci
2. Add .travis.yml file in repo
3. Add envoirment variables aws IAM user

## AWS Elasticbeanks
> **_NOTE:_** Linux look for Dockerfile and Linux2 look for docker-compose

1. Elasticbeans -> create application -> platform docker -> branch linux 
2. Benifits -> autoscaling for amount of traffic
3. it's create s3 bucket automatically (Amazon s3 -> elasticbeanstalk-region-id)
4. Create IAM user with beanstalk full access
5. beanstalk look for EXPOSE port in Dockerfile


## CheatSheet
### Initial Setup

1. Go to AWS Management Console

2. Search for Elastic Beanstalk in "Find Services"

3. Click the "Create Application" button

4. Enter "docker" for the Application Name

5. Scroll down to "Platform" and select "Docker" from the dropdown list.

6. Change "Platform Branch" to Docker running on 64bit Amazon Linux

7. Click "Create Application"

8. You should see a green checkmark after some time.

9. Click the link above the checkmark for your application. This should open the application in your browser and display a Congratulations message.

#### Change from Micro to Small instance type:

> **_Note_** that a t2.small is outside of the free tier. t2 micro has been known to timeout and fail during the build process.

1. In the left sidebar under Docker-env click "Configuration"

2. Find "Capacity" and click "Edit"

3. Scroll down to find the "Instance Type" and change from t2.micro to t2.small

4. Click "Apply"

5. The message might say "No Data" or "Severe" in Health Overview before changing to "Ok"

Add AWS configuration details to .travis.yml file's deploy script

1. Set the region. The region code can be found by clicking the region in the toolbar next to your username.

eg: 'us-east-1'

2. app should be set to the Application Name (Step #4 in the Initial Setup above)

eg: 'docker'

3. env should be set to the lower case of your Beanstalk Environment name.

eg: 'docker-env'

4. Set the bucket_name. This can be found by searching for the S3 Storage service. Click the link for the elasticbeanstalk bucket that matches your region code and copy the name.

eg: 'elasticbeanstalk-us-east-1-923445599289'

5. Set the bucket_path to 'docker'

6. Set access_key_id to $AWS_ACCESS_KEY

7. Set secret_access_key to $AWS_SECRET_KEY

#### Create an IAM User

1. Search for the "IAM Security, Identity & Compliance Service"

2. Click "Create Individual IAM Users" and click "Manage Users"

3. Click "Add User"

4. Enter any name you’d like in the "User Name" field.

eg: docker-react-travis-ci

5. Tick the "Programmatic Access" checkbox

6. Click "Next:Permissions"

7. Click "Attach Existing Policies Directly"

8. Search for "beanstalk"

9. Tick the box next to "AdministratorAccess-AWSElasticBeanstalk"

10. Click "Next:Tags"

11. Click "Next:Review"

12. Click "Create user"

13. Copy and / or download the Access Key ID and Secret Access Key to use in the Travis Variable Setup.

#### Travis Variable Setup

1. Go to your Travis Dashboard and find the project repository for the application we are working on.

2. On the repository page, click "More Options" and then "Settings"

3. Create an AWS_ACCESS_KEY variable and paste your IAM access key from step #13 above.

4. Create an AWS_SECRET_KEY variable and paste your IAM secret key from step #13 above.

#### Deploying App

1. Make a small change to your src/App.js file in the greeting text.

2. In the project root, in your terminal run:

```git add.```

```git commit -m “testing deployment"```

```git push origin master```

3. Go to your Travis Dashboard and check the status of your build.

4. The status should eventually return with a green checkmark and show "build passing"

5. Go to your AWS Elasticbeanstalk application

6. It should say "Elastic Beanstalk is updating your environment"

7. It should eventually show a green checkmark under "Health". You will now be able to access your application at the external URL provided under the environment name.
