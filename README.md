# Taas-API
TaaS API Description

API to access Topsoil Mapper cloud processed data via API. Access to the TaaS API needs an active user account at the TaaS portal. For further questions please contact support@geoprospectors.com.


Token & Data Service: https://service.geoprospectors.com:8091/API

## AUTHENTICATE

The API uses bearer token to authenticate a request. POST a mail address and the password to the token service will issue an access token.<br />
Available endpoints:

<details><summary>requestToken</summary>

https://{host service}/authenticate/requestToken (Post Request)

{<br />
“UserName”: {Username}<br />
“Password”: {password}<br />
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
</details>
<details><summary>refreshToken</summary>
<br />
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
</details>

## SERVICE ORDER

Standard data exchange endpoints can be accessed:
<br />
<details><summary>requestJobList</summary>
<br />
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
*Remark:*<br />
Properties can be left empty or flag '0' for all files. Flag '999' will return those Jobs which are processed without error.<br />
</details>

<details><summary>requestECaData</summary>
<br />
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
</details>
<details><summary>requestECaZones</summary>
<br />
https://{Host Service}/ServiceOrder/requestECaZones (Post Request)

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
{ 
“type”: “Polygon”,
	“coordinates”: {XX,YY}
	“properties”: {properties}
}
```
Example response:<br />
```
[
{"type": "FeatureCollection",
  "features": [
	{"type": "Feature",
	  "geometry": {"type": "Polygon", "coordinates": [ 47.135445,16.16.88135 …]},
	  "properties": 
		{
		"Zone": "1",
		}
	}]
}
]
```
</details>
<details><summary>AccountDetails</summary>
<br />
https://{Host Service}/ServiceOrder/AccountDetails (Post Request)

Request<br />
```
{
	“Access Token”: {Token}
	“JobID”: {JobID}
}
```
Response: {GeoJSON}<br />
```
{
	“CustNr”: {Customer Number}
	“Company”: {Company Name}
	"User Name": {User Name, first last}
	“Mail”: {mail address}
	"Region": {geographic region}
	“User Class”: {userclass number}
	"Terms": {User Terms}
	"ProductSet": {entitled products to access}
	"openArea": {area entitlement}
	“Systems”: {[System SN]}
}
```
