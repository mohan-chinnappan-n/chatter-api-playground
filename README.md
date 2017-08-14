## SFDC Chatter API playground with curl


### bash script

[sfdc_chatter.sh](./sfdc_chatter.sh)

### Steps:

1. Edit the [sfdc_chatter.sh](./sfdc_chatter.sh) to fill in your ACCESS_TOKEN

2. Play with examples shown here



### Examples in action

#### users/me
![users/me](./img/user_me.png)

------
#### Address filter
![](./img/address-filter.png)
------
#### Address filter
![](./img/photo-filter.png)
------
#### getMyNewsFeed
![](./img/getMyNewsFeed.png)		
------
#### get feed elements for the opportunity
![](./img/feedElement-for-oppty.png)
------


#### Post comment
![](./img/postComment-example.png)
------
#### Data file for posting comment [comments.json](./comment.json)
```json
{
   "body":{
      "messageSegments":[
         {
            "type":"Text",
            "text":"Another New comment from  curl "
         }
      ]
   }
}
```
------
### How it looks in the chatter page
![](./img/postComment-screen.png)

------

### References
1. [Chatter API doc](https://developer.salesforce.com/docs/atlas.en-us.chatterapi.meta/chatterapi/features.htm)
