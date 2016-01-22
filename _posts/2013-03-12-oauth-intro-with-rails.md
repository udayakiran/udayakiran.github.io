---
layout: post
title: "OAuth 2 - Introduction and Implementation with rails"
description: "Quick introduction about oauth and implementing an oauth provider in rails for an API"
tags: [ror, ruby, web]
image:
  feature: abstract-6.jpg
  color: "39b470"
  icon: "clock-o"
bg_color: "39b470"
---

This article covers basics of OAuth 2 and explains how to implement oAuth provider for authenticating a set of REST APIs. Implementation is explained keeping rails (2.3.x) in mind.

## Scope -

To provide a way for other applications to use our APIs by authenticating and authorizing through Oauth.

This should cover the following -

- Server flow as described in Oauth 2.0 (We follow v22 spec of Oauth - <http://tools.ietf.org/html/draft-ietf-oauth-v2-22>)
- Endpoint for clients to request authorization code.
- Endpoint to request an access token using the authorization code.

## OAuth 2.0 Spec & discussion -

There are 4 different types of token grant are available. We use two of them which are famous and applicable to majority of the cases.

### 1. Grant type - password


                     +--------+                                  +---------------+
                     |        |--(A)- Authorization Request ->   |  Authorization|
                     |        |       (with username, password)  |   Server      |
                     |        |<-(D)----- Access Token -------   |               |
                     |        |                                  +---------------+
                     | Client |
                     |        |                                  +---------------+
                     |        |--(E)----- API request ------>    |   Resource    |
                     |        |           (With access token)    |    Server     |
                     |        |<-(F)------ API response -------  |               |
                     +--------+                                  +---------------+


The following are the important points from our oauth implementation.

- The token exchange and authentication will happen over SSL so that the token security is not compromised.
- The access token is expired every 2 days. (This can be kept as less as possible to avoid security risks.)

- Though 'refresh_token' is recommended to regenerate access token, to keep the implementation simple in some apps, every time a token is expired user can be forced to has to enter his username and password with the client and get the access token generated.

#### Sample Oauth Request and Response -

**Request URI -** `https://api.myauthserver.com/api/authentication/token`

**Parameters -** client_id, client_secret, grant_type, username, password.

- The value of grant_type should be - passsword

- The default value of format is xml.

#### Successful authentication response -

**1. XML -**

    <oauth2-token>
      <access-token>6uJ0xn1mynyh9UZZ3gC46L8UPImLv6r9fsEWmz9T</access-token>
      <token-type>bearer</token-type>
      <expires-in>5183999</expires-in>
    </oauth2-token>

**2. JSON -**

    {"oauth2_token":
      {"token_type":"bearer",
       "expires_in":5183999,
       "access_token":"WFfKQaElw1dvNggDK4eBuiyNbrcS2xajCDs2LI2p"
      }
    }

##### Failed authentication Response -

**1. XML -**

    <api>
      <response>
        <error>
          <description>invalid_user</description>
          <error-code>ERRR00005</error-code>
        </error>
      </response>
    </api>

**2. JSON -**

    {"api":
       "response":
         {"error":  
           {"description":"invalid_user","error_code":"ERRR00005"}
         }
    }

### 2. Grant type - auth_code


                     +--------+                               +---------------+
                     |        |--(A)- Authorization Request ->|   Resource    |
                     |        |                               |     Owner     |
                     |        |<-(B)-- Authorization Grant ---|               |
                     |        |                               +---------------+
                     |        |
                     |        |                               +---------------+
                     |        |--(C)-- Authorization Grant -->| Authorization |
                     | Client |                               |     Server    |
                     |        |<-(D)----- Access Token -------|               |
                     |        |                               +---------------+
                     |        |
                     |        |                               +---------------+
                     |        |--(E)----- Access Token ------>|    Resource   |
                     |        |                               |     Server    |
                     |        |<-(F)--- Protected Resource ---|               |
                     +--------+                               +---------------+


#### Sample oAuth Requests and Response

**STEP 1:** Client app sends a request to authorize url of myauthserver -

- The Client application sends a request to the authorize url of myauthserver.

**Request URI -**

     https://api.myauthserver.com/api/authentication/oauth/authorize?response_type=code&client_id=<client_app_id>&redirect_uri=<client_app_redirect_uri>

This redirects user to a login page.

**1. On successful login and authorize -**

- The user will be redirected to `<client_app_redirect_uri>?code=W25JoW2cktPurc7vpBaI`

- The client sends a request to the token url mentioned above and receives token.

- The only difference is that the grant_type param value should be authorization_code when requesting for token.

**2. On unsuccessful login and authorize -**

- The client will be redirected to `<client_app_redirect_uri>?error=<error_description>`

- The most common error_desription will be access_denied

**STEP 2:** 1. Client app sends a request for access token-

The Client application sends a request to the token url of myauthserver.

**Request URI -** https://api.myauthserver.com/api/authentication/token

**Parameters -** client_id, client_secret, grant_type, username, password,

- The value of grant_type should be - authorization_code

- The response for this call is same as the one we have above for password grant_type.

## Implementation -

### Providing OAuth Service -

The service provision for Oauth is developed by inspiring from the plugin - <https://github.com/pelle/oauth-plugin>

This gem does not cover the complete flow but it can be used base and the tweaks can be made to incorporate it with your app flow.

#### Prerequisites -

This plugin requires oauth2 gem to be installed.
App should use restful_athentication or any other equivalent plugin.

*Note -*

One more alternative explored was - <https://github.com/ThoughtWorksStudios/oauth2_provider>

It has a cleaner design but we are not using it as it only supports version 2-09 of OAuth 2.0 spec as of the date.

### Consuming OAuth service (for clients) -

The Oauth plugin ()<https://github.com/pelle/oauth-plugin>) has some code which can be tweaked to implement a client for the Oauth service.

In addition to this we can also use the following ruby based libraries to implement clients-

<https://github.com/intridea/oauth2>

<https://github.com/aflatter/oauth2-ruby>


>> Oauth2 is the industry standard for the authentication of APIs as of now and it is recommended to use this for any web services without a second thought.
