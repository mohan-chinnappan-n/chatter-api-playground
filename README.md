## SFDC Chatter API playground with curl


#### bash script

``` bash

# filename: sfdc_chatter.sh
# Bash shell to acts as a playground to SFDC Chatter API
# resource supported:
# 1. /users/me
# 2. filter examples
# 3. getMyNewsFeed
# 4. feedElements
# 5. postComment




# Chatter API Version
version=v40.0
# your org instance url
instance=https://mohansun-lx1-dev-ed.my.salesforce.com
# chatter REST API resource URL
chatter_resource_uri_prefix=/services/data/$version/chatter
# read the ACCESS_TOKEN from the Shell
access_token=$ACCESS_TOKEN
contentType="Content-Type: application/json"

#-----------------------------------------------
## Examples
# about me
# usage:  bash sfdc_chatter.sh me  | jq

# filter is provided in $2
# get only address (filter)
#   example filter, get me the address: ?include=/aboutMe%7C/address
#   usage: bash sfdc_chatter.sh me ?include=/aboutMe%7C/address | jq
# get only photo (filter)
#   example filter, get me the photo: ?include=/aboutMe%7C/photo
#   usage: bash sfdc_chatter.sh me ?include=/aboutMe%7C/photo | jq

# usage: bash  sfdc_chatter.sh me ?include=/aboutMe%7C/photo | jq

# usage: bash  sfdc_chatter.sh  getMyNewsFeed   | jq

# usage: bash  sfdc_chatter.sh  feedElements opportunity  | jq

# usage: bash  sfdc_chatter.sh  postComment 0D5f4000003C6NuCAK  | jq
#-----------------------------------------------

filter=$2
# default HTTP VERB
VERB='GET'

# refer: https://developer.salesforce.com/docs/atlas.en-us.chatterapi.meta/chatterapi/features.htm
# open https://developer.salesforce.com/docs/atlas.en-us.chatterapi.meta/chatterapi/features.htm

# form the resource_uri based on the given  input $1
if [ $1 = 'me' ]; then
    resource_uri=$chatter_resource_uri_prefix/users/me/$filter
elif [ $1 = 'getMyNewsFeed' ]; then
    resource_uri=$chatter_resource_uri_prefix/feeds/news/me/feed-elements
elif [ $1 = 'feedElements' ]; then
    resource_uri=$chatter_resource_uri_prefix/feed-elements?q=$2
elif [ $1 = 'postComment' ]; then
    feedElementId=$2
    resource_uri=$chatter_resource_uri_prefix/feed-elements/$feedElementId/capabilities/comments/items
    VERB='POST'
    DATA_INPUT=$3
else
    resource_uri=$chatter_resource_uri_prefix/users/me
fi

#echo $resource_uri
## real action here!
if [ $VERB = 'POST' ]; then
  curl -X $VERB $instance$resource_uri \
       -H "Authorization: Bearer $access_token" -H "$contentType"  \
       -d @$DATA_INPUT
else
  curl -X $VERB $instance$resource_uri \
       -H "Authorization: Bearer $access_token"
fi

```

### Examples in action

#### users/me
![users/me](User_me.png)

![](Address-filter.png)
![](Photo-filter.png)
![](GetMyNewsFeed.png)		
![](FeedElement-for-oppty.png)
![](PostComment-screen.png)
![](Comment.json.png)
![](PostComment-example.png)
