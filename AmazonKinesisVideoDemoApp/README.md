# Running AmazonKinesisVideoStreaming Sample

More information: [https://docs.aws.amazon.com/kinesisvideostreams/latest/dg/producer-sdk-android.html](https://docs.aws.amazon.com/kinesisvideostreams/latest/dg/producer-sdk-android.html)

## 1. Create a user pool
  * Go to https://console.aws.amazon.com/cognito/
  * Click `Manage your User Pools`
  * Click `Create a user pool`
  * Fill-in `Pool name`
  * Click `Review defaults`
  * Click `Create user pool`
  * Copy `Pool Id` :clipboard:
  * Select `App clients` in the left nav.
  * Click `Add an app client`
  * Fill-in `App client name`
  * Click `Create app client`
  * Click `Show details` and copy `App client id` and `App client secret` :clipboard:
    * ![Shows show details button](screenshots/click_show_details.png) `-->` ![](screenshots/copy_app_client_id_and_secret.png)

## 2. Create an identity pool
  * Go to https://console.aws.amazon.com/cognito/
  * Click `Manage Federated Identities`
  * Click `Create new identity pool`
  * Fill-in `Identity pool name`
    * ![Shows field for inputting identity pool name](screenshots/pool_name.png)
  * Under the heading `Authentication providers`, in the `Cognito` tab, fill-in the `User Pool Id` and `App client id` from the user pools step.
    ![Shows field for inputting identity pool name](screenshots/fill_in_user_pool.png)
  * Click `Create create`
  * There will be details for 2 roles. Look at the one for `authenticated identities` and click `Edit` next to the policy document and your policy should look like this:
    ```
    {
        "Version": "2012-10-17",
        "Statement": [
          {
            "Effect": "Allow",
            "Action": [
              "cognito-identity:*",
              "kinesisvideo:*"
            ],
            "Resource": [
              "*"
            ]
          }
        ]
      }
    ```
  * Click `Allow`
  * Copy the `Identity Pool Id` from the code snippets on the screen. :clipboard:

## 3. Paste
  * You will need all the information from the above steps that have :clipboard: and paste them into this file on your local copy [awsconfiguration.json](src/main/res/raw/awsconfiguration.json). Here's what it should look like when you're done:
```json
{
  "Version": "1.0",
  "CredentialsProvider": {
    "CognitoIdentity": {
      "Default": {
        "PoolId": "us-west-2:01234567-89ab-cdef-0123-456789abcdef",
        "Region": "us-west-2"
      }
    }
  },
  "IdentityManager": {
    "Default": {}
  },
  "CognitoUserPool": {
    "Default": {
      "AppClientSecret": "abcdefghijklmnopqrstuvwxyz0123456789abcdefghijklmno",
      "AppClientId": "0123456789abcdefghijklmnop",
      "PoolId": "us-west-2_qRsTuVwXy",
      "Region": "us-west-2"
    }
  }
}
```
  * Change the region that the app will stream to by editing the `KINESIS_VIDEO_REGION` constant in your local copy of [KinesisVideoDemoApp.java](https://github.com/awslabs/aws-sdk-android-samples/blob/master/AmazonKinesisVideoDemoApp/src/main/java/com/amazonaws/kinesisvideo/demoapp/KinesisVideoDemoApp.java)


## Streaming From Your Android Camera
  * After signing in, you'll be taken to the Streaming Configuration screen.
     * Note: If this is your first time signing in, you'll need to create an account. You can do this by clicking `Create New Account` on the sign-in screen.
  * Modify these settings, or you can leave everything on the default values if you wish.
  * Click the `Start Streaming` button and check out your video on the AWS Console.

## Streaming Video Frame Files
  * After signing in, you'll be taken to the Streaming Configuration screen.
  * Click on the Hamburger icon in the top-left and in the navigation pane that pops up, choose `Stream From Assets`.
  * Modify the Stream Name if you wish, then click the `Stream Frames` button.
  * Check out the video on the AWS Console.