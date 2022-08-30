# Taas-API
TaaS API Description

API to access Topsoil Mapper cloud processed data via API (BETA Stage).

Available endpoints:
- requestTOKEN
- requestJobList
- requestECaData
- requestECaZones

Token & Data Service: https://service.geoprospectors.com:8091/API

## AUTHENTICATE

The API uses bearer token to authenticate a request. POST a mail address and the password to the token service will issue an access token.

**requestToken**

https://{host service}/authenticate/requestToken (Post Request)

{<br />
“UserName”: {Username}<br />
“pwd”: {password}<br />
}<br />
Response:<br />
```
{
	“User Name”: {User Name, first last}
	“Company”: {Company Name}
	“Systems”: {[System SN]}
	“userclass”: {userclass number}
	“Mail”: {mail address}
“Access Token”: {token}
	“CustNr”: {Customer Number}
	“issued”: {date}
	“expires”: {date}<br />
}
```

Example response:<br />
```
{
"User Name":"Max Mustermann",
"Company":"Muster GmbH",
"Systems":["TSM-000","TSM-001"],
"userclass":"5",
"Mail":"mm@geoprospectors.com",
"Access Token":"W7M4ABoaGhoiAfDdnDlwqHXKqLzs5dN5Spq5lE2108jPC7ZIXiop
+HDUHZCmGavE\n1nUFYwp/U+W/u//PhqAZ6+                   vOkLJpcbslUYU4NLUqsCnQxnbOqTx9kCsuJxaCs/+
		      I\n+rPVuJVaDX8VCZ30ObaTwrmDU2YWanS4VXLX",
"CustNr":"1",
"issued":"01.10.2021-13:12",
"expires":"01.10.2021-13:22"<br />
}
```

**refreshToken**

https://{host service}/authenticate/requestToken (Post Request)

Request
```
{
	“Access Token”: {Token}
}
```
Response:
```
{
	“status”: {[Status]}
}
```
Example response:
```
{
	Tokenupdated
 }
```

## SERVICE ORDER

**requestJobList**

https://{Host Service}/ServiceOrder/requestJobList (Post Request)

Request

```
{
	“Access Token”: {Token}
	“SN”: {Serial Number}
	“selector”: {number}
}
```
Response: {GeoJSON}
```
{ 
“type”: “Point”,
	“coordinates”: {XX,YY}
	“properties”: {properties
}

Example response:

[
{"type": "FeatureCollection",
  "features": [
	{"type": "Feature",
	  "geometry": {"type": "Point", "coordinates": [ 47.135445,16.16.88135]},
	  "properties": 
		{
		"JobID": "177",
		"Field Name": "Testfield",
		"Area": "23.15",
		"Date": "09/08/2020/13:11:31,4"
		}
	}]
}
]
```

**requestECaData**

https://{Host Service}/ServiceOrder/requestECaData (Post Request)

***remark:*** only those JobIDs with the corresponding user privileges (Serial Number) can be requested. Valid Serial Number per user can be request wile Token request.

Request<br />
```
{
	“Access Token”: {Token}
	“JobID”: {JobID}
}
```
Response: {GeoJSON}<br />
```
“type”: “Point”,
	“coordinates”: {XX,YY}
	“properties”: {properties}
```

Example response:<br />
```
[
{"type": "FeatureCollection",
  "features": [
	{"type": "Feature",
	  "geometry": {"type": "Point", "coordinates": [ 47.135445,16.16.88135]},
	  "properties": 
		{
		"ECaR1": "8.1",
		"ECaR2": "12.2",
		"ECaR3": "14.8",
		"ECaR4": "17.4"
		}
	}]
}
]
```

