Connects to Facebook from Ballerina.

# Package Overview
The Facebook connector allows you to create retrieve and delete posts through the Facebook Graph API. It handles OAuth 2.0 authentication.

**Post Operations**

The `keerthu/facebook` package contains operations to create, get and delete posts.

## Compatibility

|                                 |       Version                  |
|  :---------------------------:  |  :---------------------------: |
|  Ballerina Language             |   0.970.0                      |
|  Facebook API                   |   v2.12                        |

## Sample

First, import the `keerthu/facebook` package into the Ballerina project.

```ballerina
import keerthu/facebook;
```

Instantiate the connector by giving authentication details in the HTTP client config. The HTTP client config has built-in support for BasicAuth and OAuth 2.0. Facebook uses OAuth 2.0 to authenticate and authorize requests. The Facebook connector can be instantiated in the HTTP client config using the access token.


**Obtaining Tokens to Run the Sample**
Login into [Graph API Explorer](https://developers.facebook.com/tools/explorer/) and get the access token.

You can now enter the credentials in the HTTP client config:
```ballerina
endpoint facebook:Client facebookEP {
    clientConfig:{
        auth:{
            accessToken:accessToken
        }
    }
};
```

The `createPost` function creates a post for a user, page, event, or group.
```ballerina
//Create post.
var response = facebookEP->createPost(id,message,link,place);
```

The response from `createPost` is a `Post` object if the request was successful or a `FacebookError` on failure. The `match` operation can be used to handle the response if an error occurs.
```ballerina
match response {
   //If successful, returns the Post object.
   facebook:Post fbRes => io:println(fbRes);
   //Unsuccessful attempts return a FacebookError.
   facebook:FacebookError err => io:println(err);
}
```

The `retrievePost` function retrieves the post specified by the ID. The `postId` represents the ID of the post to be retrieved. It returns the `Post` object on success and `FacebookError` on failure.
```ballerina
var fbRes = facebookEP.retrievePost(postId);
match fbRes {
    facebook:Post p => io:println(p);
    facebook:FacebookError e => io:println(e);
}
```

The `deletePost` function deletes the post specified by the ID. The `postId` represents the ID of the post to be deleted. It returns the `True` object on success and `FacebookError` on failure.
```ballerina
var fbRes = facebookEP.deletePost(postId);
match fbRes {
    boolean b => io:println(b);
    facebook:FacebookError e => io:println(e);
}
```
