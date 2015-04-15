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

#### <a name="store-object-inquiry">Store Object Inquiry</a>    

|Resource URI                 |
|:----------------------------| 
|/v4/couponapp/store          |

   Resource Properties    
   
   Property	Value	Mandatory	Description

#### <a name="coupon-object-inquiry">Coupon Object Inquiry</a>

|Resource URI                 |
|:----------------------------| 
|/v4/couponapp/coupon         |


    	Resource Properties
    	Property	Value	Mandatory	Description

#### <a name="store-object-search">Store Object Search</a>

|Resource URI                 |
|:----------------------------| 
|/v4/couponapp/search         |

    	Resource Properties
    	Property	Value	Mandatory	Description

#### <a name="update-coupon-save-count">Update Coupon Save Count</a>

|Resource URI                 |
|:----------------------------| 
|/v4/couponapp/saveCoupon     |

		Resource URI
        /v4/couponapp/saveCoupon

    	Resource Properties
    	Property	Value	Mandatory	Description
