# Tags

## Edit or delete

This endpoint will edit or delete a tag.

This endpoint resembles a scenario when an user wants to a. Add a new tag, b. edit an existing tag or c. delete an existing tag.

```shell
# HTTP REQUEST BODY

{ 
	"tagtoapply":"new tag",
	"tagtype":"
}
```

> The above request should return following header

```shell

Location: http://path_to_api/api/noteitem?id=5392dcf623aea51b4cded7c6

```

### HTTP Request

`POST api/Tags/EditDelete`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST BODY PARAMETERS

Parameter | Description
-------------- | --------------
tagtoapply | **optional** <i>- 3 to 50 characters long </i> <br> title of note item
tagtodelete | **optional** <i>- 3 to 250 characters long </i> <br> description of note item 
tagtype | **required** <br> tag associated with <br> ***supported values*** - lineitem, noteitem, template, recipient, recipientcompany, attachment
itemid | **optional** <i>- 4 to 25 characters long </i> <br> name of group to which the note item belongs to

### HTTP Response

<aside class="success">
201 Created
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>

## Rearrange

This endpoint will re-arrange an existing list of tags as per the tag type provided.

This endpoint resembles a scenario when an user wants to re-arrange (re-position) a list of tags as per tag type provided.

> The request should return the following JSON

```shell
# HTTP RESPONSE OBJECT

{
	"tagtype":"lineitem",
	"Tags":
	[
		"sample",
		"note item"
	]
}

```

### HTTP REQUEST

`GET api/Tags/Rearrange`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST ARGUMENTS

Argument | Description
-------------- | --------------
tagtype | **required** <br> type of tags to re-arrange <br> **supported values:** LineItem, NoteItem, Template, Recipient, RecipientCompany, Attachment
tags | **required** <br> model for list of tags to rearrange

### HTTP Response 

<aside class="success">
200 OK
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>
