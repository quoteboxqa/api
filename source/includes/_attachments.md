# Attachment

## Get upload URI

This endpoint will get an upload URI to upload attachments associated with an account.

You'll need an upload uri for reference of actual files uploaded to our Azure storage, or you'll keep looking for them and would get just nothing later on. Don't blame it on us then.

> The request should return the following response

```shell

{
	"UploadUri":"https://quoteappstorage.blob.core.windows.net/53984e1f23aea51f8ce5b020/{0}/?sv=2014-02-14&sr=c&sig=bYUtFSggbIgtBOYMrauglq1hvNz%2BSppangcVB%2FhmbNs%3D&st=2014-06-11T12%3A35%3A13Z&se=2014-06-11T22%3A40%3A13Z&sp=w",
	"Errors":[]
}

```

### HTTP Request

`GET api/Attachment/GetUploadUri`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

<aside class="success">
200 Ok
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>

## Create attachment

This endpoint will create a new attachment of the specified type.

```shell

# HTTP REQUEST OBJECT

{
	"OriginalUri":"https://quoteappstorage.blob.core.windows.net/53984e1f23aea51f8ce5b020/demo-image-1.png",
	"Type":"Image",
	"FileName":"demo-image-1.png",
	"Caption":"sample",
	"InLibrary":true,
	"Tags":
	[
		"sample",
		"attachments"
	]
}

```

### HTTP Request

`POST api/Attachment/Create`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST BODY PARAMETERS

Parameter | Description
-------------- | --------------
originaluri | **required** <br> actual uri of file stored to blob storage
type | **required** <br> type of attachment <br> ***supported values:*** image, document, video, virtualtour
filename | **required** <br> real name of the file uploaded along with its extension
caption | **required** <br> caption for file, can be the file name itself or another piece of text to identify the file by text
inlibrary | **optional** <i>- boolean, default false, should be true if the file is to be saved in library <br> property to identify if the file is an attachment for line/note item or a file in library associated with an account
tags | **optional** <br> model for list of tags associated with the file

<aside class="success">
200 Ok
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>

## Update caption

This endpoint will update caption of an existing attachment.

```shell

# HTTP REQUEST OBJECT

{
	"AttachmentId":"5396b4d423aea51f4cbdabbc",
	"Caption":"edited sample",
}

```

### HTTP Request

`POST api/Attachment/Update`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST BODY PARAMETERS

Parameter | Description
-------------- | --------------
attachmentid | **required** <br> id of the attachment to update the caption
caption | **required** <i>- 3 to 50 characters long</i> <br> caption for file, can be the file name itself or another piece of text to identify the file by text

<aside class="success">
200 Ok
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>

## Get attachment

This endpoint will get an attachment.

```shell

# HTTP RESPONSE BODY

{
	"AttachmentItem":
	{
		"Id":"5396b4d423aea51f4cbdabbc",
		"Type":0,
		"Uuid":null,
		"FileName":"635365301610919762_SAM_6517.JPG",
		"Uris":null,
		"ThumbUri":null,
		"DownloadUri":"http://quoteappstorage.blob.core.windows.net/5379f08d4ac4891554896e7c/635365301610919762_SAM_6517.JPG",
		"InLibrary":true,
		"Caption":"my file"
	},
	"Errors":[]
}

```

### HTTP Request

`GET api/Attachment?id=5396b4d423aea51f4cbdab43`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST BODY PARAMETERS

Parameter | Description
-------------- | --------------
id | **required** <br> id of the attachment to get

<aside class="success">
200 Ok
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>

## Search attachment

This endpoint will search an attachment of specified type with advanced filters (if applied).

```shell

# HTTP REQUEST OBJECT

{
	"Type":"Image",
	"Key":"sample",
	"GetTags":false
}

```

> The above request should return following JSON

```shell

{
	"Attachments":
	[
		{
			"Id":null,
			"Type":0,
			"Uuid":null,
			"FileName":
			"635365301610919762_SAM_6517.JPG",
			"Uris":null,
			"ThumbUri":null,
			"DownloadUri":"http://quoteappstorage.blob.core.windows.net/5379f08d4ac4891554896e7c/635365301610919762_SAM_6517.JPG",
			"InLibrary":false,
			"Caption":"my file"
		}
	],
	"Tags":null,
	"Errors":[],
	"PageNumber":1,
	"PageSize":10,
	"TotalCount":1,
	"TotalPages":1,
	"HasPreviousPage":false,
	"HasNextPage":false
}

```

### HTTP Request

`POST api/Attachment/Search`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST BODY PARAMETERS

Parameter | Description
-------------- | --------------
id | **required** <br> id of the attachment to get

<aside class="success">
200 Ok
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>

## Delete attachment

This endpoint will delete an attachment.

```shell

# HTTP REQUEST OBJECT

{
	"AttachmentsIdList":
	[
		"",
		"",
		...
	],
	"DeleteFromLibrary":true
}

```

### HTTP Request

`POST api/Attachment/Delete`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST BODY PARAMETERS

Parameter | Description
-------------- | --------------
AttachmentsIdList | **required** ***- minimum 1 attachment id is required*** <br> model for list of attachment id to delete
DeleteFromLibrary | **optional** ***- boolean*** <i>, default false, true if want to delete the attachment from library </i> <br> property to set if attachment needs to be deleted from library

<aside class="success">
200 Ok
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>

## Get document view session id

This endpoint will get session id associated for a document attachment type associated with an account.

> The request should return the following JSON

```shell

# HTTP RESPONSE OBJECT

{
	"SessionId":"73a0c0ee20ab49d48934c6fe688012b6",
	"Errors":[]
}

```

### HTTP Request

`GET api/Attachment/GetDocument?id=5396b4d423aea51f4cbdabbc`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST BODY

Parameter | Description
-------------- | --------------
id | **required** <br> UUID of document attachment

<aside class="success">
200 Ok
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>