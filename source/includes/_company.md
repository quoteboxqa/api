# Recipient (company)

## Create or update

This endpoint will create or update a recipient (company).

This endpoint resembles a scenario when an user wants to either create a new recipient (company) or update an existing recipient (company).

```shell
# HTTP REQUEST BODY

{
	"companyname":"Globotmantics",
	"email":"contact@globomantics.com",
	"phones":
	[
		{
			"type":"primary",
			"value":"+910123456789"
		}
	],
	"address":
	[
		{
			"addressline1":"stree1",
			"addressline2":"street2",
			"city":"New York",
			"zip":"10001",
			"addresstype":"primary",
			"country":"USA"
		}
	],
	"tags":
	[
		"ny contacts",
		"ca"
	]
}
```

> The above request should return following header

```shell

Location: http://path_to_api/api/recipient?id=5392dcf623aea51b4cded7c6&type=company

```

### HTTP Request

`POST api/Recipient/CreateUpdateCompany`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST BODY PARAMETERS

Parameter | Description
-------------- | --------------
companyname | **required** <i>- 3 to 25 characters long </i> <br> company name
email | **required** <i>- 10 to 65 characters long </i> <br> email of recipient-company
phones | **optional** <br> model for list of phone numbers associated with the recipient-company
addresses | **optional** <br> model for list of addresses associated with the recipient-company
tags | **optional** <br> model for list of tags associated with the recipient-company

### HTTP Response

<aside class="success">
201 Created
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>

## Archive

This endpoint will archive recipient(s) (company).

This endpoint resembles a scenario when an user wants to archive recipient(s) (company).

```shell
# HTTP REQUEST BODY

{
	"recipientcompanyids":
	[
		"537d82b423aea5226cc52e65",
		"537d82b323aea5226cc52e64",
		...
	]
}
```

### HTTP REQUEST

`POST api/Recipient/Archive`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST PARAMETERS

Parameter | Description
-------------- | --------------
recipientcompanyids | **minimum 1 recipient-company id required** <br> list of recipient-company ids to archive

### HTTP Response 

<aside class="success">
200 OK
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>

## Clean up

This endpoint resembles a scenario when an user wants to quickly delete all recipient(s) (person & companies) associated with his/her account with whom no quotes (irrespective of the type) are associated.

```shell
# HTTP REQUEST BODY

{}

```

>  The above request should return following JSON

```shell
# HTTP RESPONSE OBJECT

{
	"deletedrecipient-companycount":0,
	"deletecompaniescount":2
}

```

### HTTP REQUEST

`POST api/Recipient/CleanUp`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP Response 

<aside class="success">
200 OK
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside> 