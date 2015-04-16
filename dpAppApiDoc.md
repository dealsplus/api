# Getting Started    
This page contains the basic concepts and data formats of the Dealsplus Coupon API.    

* [Structure of the REST URL](#structure-of-the-rest-url)    
* [Authentication](#authentication)    
* [Request Formats](#request-format)    
* [Response Formats](#response-format)    
* [API Request Resource](#api-request-resource)    
	* [Store Object Inquiry](#store-object-inquiry)
	* [Coupon Object Inquiry](#coupon-object-inquiry)
	* [Store Object Search](#store-object-search)
	* [Update Coupon Save Count](#update-coupon-save-count)
	* [Update Store Save Count](#update-store-save-count)
	* [Terms of Use Inquiry](#terms-of-use-inquiry)
	* [Privacy Policy Inquiry](#privacy-policy-inquiry)      
* [API Request URL](#api-request-url)
 	* [Store Selection Page](#store-selection)
 	* [Home Page](#home)
 	* [Popular Page](#popular)
	* [My Store Page](#my-store)
	* [Search Store Page](#search-store)
	* [Store page](#store)
	* [Saved Coupon Page](#update-coupon-save-count)
	* [Terms of Use Page](#terms-of-use)
	* [Privacy Policy Page](#privacy-policy)  

## <a name="structure-of-the-rest-url">Structure of the REST URL</a>
URLs for Dealsplus REST API have the following structure:

|URL Structure                             |
|:-----------------------------------------|    
|http://api.dealsplus.com/{Request API URL}|


#### Example of URL for Store Object Inquiry
|Example URL|
|:----------|  
|http://api.dealsplus.com/v4/couponapp/store|

## <a name="authentication">Authentication</a>
All requests made to the Dealsplus Coupon App API requires an encoded API Key that is assigned to the app for Authentication.    
To pass the API Key, you need to simply pass it in the URL as the 'key' parameter.


|URL Structure with Authentication Credentials|   
|:-----------------------------------------|   
|http://api.dealsplus.com/{Request API URL}?key={YourAPIKey}|

#### Example of URL for Coupon Object Inquiry with API Key
|Example URL|
|:-----------------------------------------|      
|http://api.dealsplus.com/v4/couponapp/coupon?key=abcdefghijklmnopqrstuvwxyz|

## <a name="request-format">Request Formats</a>
The REST Request Format for all APIs is a simple HTTP GET action. By default, REST requests send a REST JSON response.     
    
#### Example Request    

```
GET /v4/couponapp/store?key={YourAPIKey}&pageSize=20&page=1
```
## <a name="response-format">Response Formats</a>
The response from our REST APIs requests is in REST JSON response format.      
    
#### Example Response    

```
{
    "msg": "",
    "errorCode": 0,
    "error": false,
    "results": true,
    "count": 2,
    "coupons": [
        {
            "storeId": 21,
            "storeName": "Macy's",
            "storeLogo": "http://img.dealspl.us/dealimage/stores/orig/0/macys.com_1410986359.jpg",
            "coverImage": "http://img.dealspl.us/dealimage/coupon/med/97/971796_1429211548.jpg",
            "couponId": 971796,
            "expireTime": "05/17/2033",
            "expireCopy": "limited time",
            "title": "Printable Coupon: $10 Off Purchase of $75+",
            "description": "",
            "type": "inStore",
            "subType": "printable",
            "printableImage": "http://www.dealsplus.com/images/coupon/41/macys-coupons_41920.jpg",
            "imageType": "jpg",
            "shareCopy": "Hey check out this sale! Printable Coupon: $10 Off Purchase of $75+ at Macy's. http://www.dealsplus.com/macys-coupons?code=971796"
        },
        {
			  ...
        }
    ]
}
```
## <a name="api-request-resource">API Request Resource</a>

### <a name="store-object-inquiry">Store Object Inquiry</a>    

####Resource URI

```
/v4/couponapp/store
```

####Resource Properties
Below are all the available properties of the Store Object Inquiry entity.    
   
|Property|Value|	Mandatory|	Description|
|:-----|:-----|:-------|:-----------|
|storeId|Integer|Yes|The Unique Store ID(s). For Multiple IDs, Seperate with '\|'. |
|excludeStores|Integer|No|Only set this field to 1 if you want to exclude the storeId(s) you passed. Otherwise, do Not pass it in your request.|
|recentHistory|Integer|No|Only set this field to 1 if you want to fetch recently visited stores with the storeId(s) you passed, it will return Store Objects in the order you passed. Otherwise, do Not pass it in your request.|
|page|Integer|No|Page Number. Default: 1| 
|pageSize|Integer|No|How many Store Objects per Page. Default: 45| 

#####Example Request
Get the first page of size 20 of all store objects except for storeId 347, 127 and 564.

```
/v4/couponapp/store?key={YourAPIKey}&storeId=347|127|564&excludeStore=1&page=1&pageSize=20
```

####Response Properties
Below are all the available properties of the Store Object Inquiry response.    
   
|Property|Value|	Mandatory|	Description|
|:-----|:-----|:-------|:-----------|
|storeId|Integer|Yes|The Unique Store ID|
|storeName|String|Yes|The Store Name|
|storeLogo|String|Yes|The URL of the Store Logo| 
|storeUrl|String|Yes|The URL of the Store Page on Dealsplus|

#####Example Response

```
{
    "msg": "",
    "errorCode": 0,
    "error": false,
    "results": true,
    "count": 3,
    "stores": [
        {
            "storeId": 9,
            "storeName": "Best Buy",
            "storeLogo": "http://img.dealspl.us/dealimage/stores/orig/0/bestbuy.com_1326387793.gif",
            "storeUrl": "http://www.dealsplus.com/bestbuy-coupons"
        },
        {
       		...
        },
        {
       		...
        }
    ]
}
```

### <a name="coupon-object-inquiry">Coupon Object Inquiry</a>

####Resource URI

```
/v4/couponapp/coupon
```
####Resource Properties
Below are all the available properties of the Store Object Inquiry entity.    
   
|Property|Value|	Mandatory|	Description|
|:-----|:-----|:-------|:-----------|
|couponId|Integer|No|The Unique Coupon ID(s). For Multiple Coupons, Seperate the IDs with '\|'.|
|storeId|Integer|No|The Unique Store ID(s). For Multiple Storess, Seperate the IDs with '\|'|
|type|String|No|Coupon Type: "online" or "inStore"| 
|expireSoon|Integer|No|Pass this parameter with '1' to get Coupons that will expire soon.| 
|page|Integer|No|Page Number. Default: 1| 
|pageSize|Integer|No|How many Coupon Objects per Page. Default: 10| 


#####Example Request
Get Coupon Objects for the saved Coupon IDs: 347, 127 and 564.

```
/v4/couponapp/coupon?key={YourAPIKey}&couponId=347|127|564
```


####Response Properties
Below are all the available properties of the Coupon Object Inquiry response.    
   
|Property|Value|	Mandatory|	Description|
|:-----|:-----|:-------|:-----------|
|couponId|Integer|Yes|The Unique Coupon Id|
|storeId|Integer|Yes|The Store Id that the Coupon belongs to|
|storeName|String|Yes|The Store Name that the Coupon belongs to| 
|storeLogo|String|Yes|The Store Logo Url that the Coupon belongs to| 
|type|String|Yes|Coupon Type: "online" or "inStore"|
|subType|String|Yes|SubType of the Coupon. For online Coupons, it's "sale" or "code"; For in-store Coupons, it's "printable" or "sale".|  
|couponCode|String|No|Coupon Code. It only gets returned if coupon type is "online" and subType is "code".| 
|title|String|Yes|Coupon Title| 
|description|String|Yes|Coupon Description| 
|link|String|Yes|The redirect URL of this Coupon.| 
|expireTime|String|Yes|The expire time of this Coupon in mm/dd/YYYY format.| 
|expireCopy|String|Yes|The text copy of this Coupon to display at the Expiration section.| 
|coverImage|String|Yes|The Cover Image URL of this Coupon.| 
|printableImage|String|No|Url of printable Coupon Image. It only gets returned if coupon type is "inStore" and subType is "printable".| 
|shareCopy|String|Yes|Text to send when sharing a Coupon|

#####Example Response

```
{
    "msg": "",
    "errorCode": 0,
    "error": false,
    "results": true,
    "count": 2,
    "coupons": [
        {
            "storeId": 21,
            "storeName": "Macy's",
            "storeLogo": "http://img.dealspl.us/dealimage/stores/orig/0/macys.com_1410986359.jpg",
            "coverImage": "http://img.dealspl.us/dealimage/coupon/med/97/971796_1429211548.jpg",
            "couponId": 971796,
            "expireTime": "05/17/2033",
            "expireCopy": "limited time",
            "title": "Printable Coupon: $10 Off Purchase of $75+",
            "description": "",
            "type": "inStore",
            "subType": "printable",
            "printableImage": "http://www.dealsplus.com/images/coupon/41/macys-coupons_41920.jpg",
            "imageType": "jpg",
            "shareCopy": "Hey check out this sale! Printable Coupon: $10 Off Purchase of $75+ at Macy's. http://www.dealsplus.com/macys-coupons?code=971796"
        }
        {
			...
        }
    ]
}
```

### <a name="store-object-search">Store Object Search</a>

####Resource URI

```
/v4/couponapp/search
```

####Resource Properties
Below are all the available properties of the Store Object Inquiry entity.    
   
|Property|Value|	Mandatory|	Description|
|:-----|:-----|:-------|:-----------|
|keyword|String|Yes|The store name keyword that user is trying to search for.|

#####Example Request
Get Store Objects match the keyword "best".

```
/v4/couponapp/search?key={YourAPIKey}&keyword=best
```

####Response Properties
Below are all the available properties of the Coupon Object Inquiry response.   

|Property|Value|	Mandatory|	Description|
|:-----|:-----|:-------|:-----------|
|storeId|Integer|Yes|The Unique Store ID|
|storeName|String|Yes|The Store Name|
|storeLogo|String|Yes|The URL of the Store Logo|
|storeUrl|String|Yes|The URL of the Store Page on Dealsplus| 

#####Example Response

```
{
    "msg": "",
    "errorCode": 0,
    "error": false,
    "results": null,
    "stores": [
        {
            "storeId": 9,
            "storeName": "Best Buy",
            "storeLogo": "http://img.dealspl.us/dealimage/stores/orig/0/bestbuy.com_1326387793.gif",
            "storeUrl": "http://www.dealsplus.com/bestbuy-coupons"
        },
        {
			...
        }
    ]
}
```

### <a name="update-coupon-save-count">Update Coupon Save Count</a>

####Resource URI

```
/v4/couponapp/saveCoupon
```

####Resource Properties
Below are all the available properties of the Coupon Save Count Update entity.   

|Property|Value|	Mandatory|	Description|
|:-----|:-----|:-------|:-----------|
|couponId|Integer|Yes|The Unique Coupon ID that the user saved.|
|delete|Integer|No|Pass 1 to this paramter if user deletes the coupon|
 
#####Example Request
Update Save Count for Coupon with ID 861.

```
/v4/couponapp/saveCoupon?key={YourAPIKey}&couponId=861
```

####Response Properties
Response returns true/false on success or error with message.

#####Example Response

```
{
    "error": false,
    "msg": "Coupon Save Count Updated!"
}
```    

### <a name="update-store-save-count">Update Store Save Count</a>

####Resource URI

```
/v4/couponapp/saveStore
```

####Resource Properties
Below are all the available properties of the Coupon Save Count Update entity.   

|Property|Value|	Mandatory|	Description|
|:-----|:-----|:-------|:-----------|
|storeId|Integer|Yes|The Unique Store ID(s) that the user saved. For Multiple IDs, add '\|' in between IDs.|
|delete|Integer|No|Pass 1 to this paramter if user deletes the coupon|
 
#####Example Request
Update Save Count for Store #78 & Store #21.

```
/v4/couponapp/saveCoupon?key={YourAPIKey}&storeId=78|21
```

####Response Properties
Response returns true/false on success or error with message.

#####Example Response

```
{
    "error": false,
    "msg": "Store Save Count Updated!"
}
```    


### <a name="terms-of-use-inquiry">Term of Use Inquiry</a>
This API Request will return Terms of Use as a string with html encoded characters.
####Resource URI

```
/v4/couponapp/term
```

####Response Properties
Response returns true/false on success or error.

#####Example Response

```
{
	msg: "",
	errorCode: 0,
	error: false,
	results: "&lt;p&gt;To better serve you and to clarify our service, we have drawn up an agreement of our terms and conditions. In order to use our service, you must read and accept all of the terms and conditions of this agreement and in the Privacy Policy. If you do not agree to be bound by the terms after you read this Agreement, you may not use our service.&lt;/p&gt;&lt;br&gt; &lt;h3&gt;1. The Service and Terms&lt;/h3&gt; &lt;p&gt; Fusion Web, LLC (referred to hereafter 
}
```    

### <a name="privacy-policy-inquiry">Privacy Policy Inquiry</a>
This API Request will return Privacy Policy as a string with html encoded characters.
####Resource URI

```
/v4/couponapp/privacy
```

####Response Properties
Response returns true/false on success or error.

#####Example Response

```
{
	msg: "",
	errorCode: 0,
	error: false,
	results: "&lt;p&gt;Here at dealsplus we recognize that your privacy is very important, and to keep you informed about our privacy practices we ask that you please read the guidelines described below. Keep in mind that because dealsplus is a growing website and internet technologies are constantly evolving, these guidelines are subject to change and any said changes will be posted on this page. Any material changes from current practices will be posted on the main page of this website to see ..." 
}
```    

## <a name="api-request-url">API Request URL</a>
This section lists all the API Request URLs with parameters for all pages on the app. All pages that requires an api call on the app are listed here.


### <a name="store-selection">Store Selection Page</a>
```
/v4/couponapp/store
```

### <a name="home">Home Page</a>
```
/v4/couponapp/coupon?storeId={savedStoreId1|savedStoreId2|...}
```

### <a name="popular">Popular Page</a>
```
/v4/couponapp/coupon
```

### <a name="my-store">My Store Page</a>
#####My Store Section
```
/v4/couponapp/store?storeId={savedStoreId1|savedStoreId2|...}
```
#####Suggested Store Section
```
/v4/couponapp/store?storeId={savedStoreId1|savedStoreId2|...}&excludeStores=1
```
### <a name="search-store">Search Store Page</a>
#####Search Result & Search Auto-Complete
```
/v4/couponapp/search?keyword={yourSearchKeyWord}
```
#####Recently Visited Stores
```
/v4/couponapp/store?storeId={savedStoreId1|savedStoreId2|...}&recentHistory=1
```

### <a name="store">Store page</a>
#####ALL Tab
```
/v4/couponapp/coupon?storeId={storeId}
```
#####ONLINE Tab
```
/v4/couponapp/coupon?storeId={storeId}&type=online
```
#####IN-STORE Tab
```
/v4/couponapp/coupon?storeId={storeId}&type=instore
```

### <a name="saved-coupon">Saved Coupon Page</a>
#####ALL Tab
```
/v4/couponapp/coupon?couponId={savedCouponId1|savedCouponId2|...}
```
#####Expiring Tab
```
/v4/couponapp/coupon?couponId={savedCouponId1|savedCouponId2|...}&expireSoon=1
```

### <a name="term-of-use">Terms of Use Page</a>
```
/v4/couponapp/term
```

### <a name="privacy-policy">Privacy Policy Page</a>
```
/v4/couponapp/privacy
```

