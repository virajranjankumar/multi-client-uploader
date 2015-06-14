# Multi Client Resumable Uploader

__!! Warning this is still buggy, but gets the main job done !!__

## Motivation
The user can upload a file, from multiple locations and networks. The idea is to speed up a user's upload if they have access to multiple networks, such as one at home, a mobile data plan and one at work. This way one file can be concurrently uploaded from multiple locations.

## Design document

The main idea is the use of a global *Ticket* board, from which mutiple clients will mark off existing parts of the upload that need to be worked on. After uploading a 5MB chunk of the file, they mark the global ticket as done, and pick off the next ticket. Once all the chunks of the file are sent to S3, complete the upload by sending a complete message to S3, which will assemble the file.

![img_20150614_124131](https://cloud.githubusercontent.com/assets/1356695/8148080/41a24e52-129b-11e5-96b6-c104e32612ff.jpg)

## Constraints
- The challenge was to write a multi-client resumable uploader, which was server light and heavier on the client side. I did this as a challenge to use Amazon Lambda, Cognito and S3, with out needing to use an EC2 instance.

- I also wanted to try out the new Promises api now shipping with major browsers.

- The users' identity management is taken care of Cognito, therefore if the user log's in on many machines / browser, I will be able to consolidate their upload.

- Amazone Lambda, will be used to notify the user when the file has been completely uploaded.

## Snapshots of Uploader
These are some snapshots of the upload process from my browser. Warning, the software is buggy.
![first](https://cloud.githubusercontent.com/assets/1356695/8148030/d1daa08a-1298-11e5-96d4-74307754e419.png)
![second](https://cloud.githubusercontent.com/assets/1356695/8148031/d1dceff2-1298-11e5-97b5-958281c92bab.png)
![third](https://cloud.githubusercontent.com/assets/1356695/8148033/d1def428-1298-11e5-9565-a70afbceb5a3.png)
![fourth](https://cloud.githubusercontent.com/assets/1356695/8148032/d1de5a72-1298-11e5-8d53-26e1a3ec4ed0.png)
![fifth](https://cloud.githubusercontent.com/assets/1356695/8148087/baa62260-129b-11e5-8426-0f4dfe16ed2c.png)
