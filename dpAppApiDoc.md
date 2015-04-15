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
            "storeId": 78,
            "storeName": "abcink",
            "storeLogo": "http://img.dealspl.us/dealimage/stores/orig/0/abcink.gif",
            "coverImage": "http://img.dealspl.us",
            "couponId": 861,
            "expireTime": 2000000000,
            "title": "",
            "description": "",
            "type": "online",
            "link": "http://www.dealsplus.com/rb2.php?cid=861",
            "couponCode": "ABC-ALL5PER",
            "subType": "code"
        },
        {
            "storeId": 567,
            "storeName": "Threadsmith",
            "storeLogo": "http://img.dealspl.us/dealimage/stores/orig/0/threadsmith.gif",
            "coverImage": "http://img.dealspl.us",
            "couponId": 5097,
            "expireTime": 2000000000,
            "title": "",
            "description": "",
            "type": "online",
            "link": "http://www.dealsplus.com/rb2.php?cid=5097",
            "couponCode": "DEQDKTCLLS6Y",
            "subType": "code"
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
|page|Integer|No|Page Number| 
|pageSize|Integer|No|How many Store Objects per Page. Default: 100| 

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
            "storeLogo": "http://img.dealspl.us/dealimage/stores/orig/0/bestbuy.com_1326387793.gif"
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
|expireTime|Integer|Yes|The expire time of this Coupon in unix timestamp format.| 
|coverImage|String|Yes|The Cover Image URL of this Coupon.| 
|printableImage|String|No|Url of printable Coupon Image. It only gets returned if coupon type is "inStore" and subType is "printable".| 

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
            "storeId": 78,
            "storeName": "abcink",
            "storeLogo": "http://img.dealspl.us/dealimage/stores/orig/0/abcink.gif",
            "coverImage": "http://img.dealspl.us",
            "couponId": 861,
            "expireTime": 2000000000,
            "title": "",
            "description": "",
            "type": "online",
            "link": "http://www.dealsplus.com/rb2.php?cid=861",
            "couponCode": "ABC-ALL5PER",
            "subType": "code"
        },
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
            "storeLogo": "http://img.dealspl.us/dealimage/stores/orig/0/bestbuy.com_1326387793.gif"
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
Below are all the available properties of the Coupon Object Inquiry entity.   

|Property|Value|	Mandatory|	Description|
|:-----|:-----|:-------|:-----------|
|couponId|Integer|Yes|The Unique Coupon ID that the user saved.|
 
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
    "msg": "Coupon Save Coupon Updated!"
}
```