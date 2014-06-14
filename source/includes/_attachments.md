# Attachment

## Get upload URI

This endpoint will get an upload URI to upload attachments associated with an account.

This endpoint resembles a scenario when an user wants to upload an attachment, to provision upload, the user needs to make a request to get the upload uri associated to his/her account, which in turn is required to create an attachment in the Create attachment action specified.

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

## Create

This endpoint will create a new attachment of the specified type.

This endpoint resembles a scenario when the system will create an attachment (save the attachment details to the database), once the uploading of the file was successful.

**Note:** </br><ul><li>If the attachment is uploaded directly to the library section, pass "InLibrary":true in the request as shown in the example.</li> <li> Also ensure the type of attachment matches the file type uploaded.</li></ul>

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

## Update

This endpoint will update caption of an existing attachment.

This endpoint resembles a scenario when an user wants to edit the caption associated with an attachment.

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

## Get

This endpoint will get an attachment.

This endpoint resembles a scenario when an user wants to view an existing attachment.

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

## Search

This endpoint will search an attachment of specified type with advanced filters (if applied).

This endpoint resembles a scenario when an user wants to search an attachment from a list of attachments for the specified type of attachment.

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

## Delete

This endpoint will delete an attachment.

This endpoint resembles a scenario when an user wants to delete an attachment/attachment(s) from an existing list of attachments.

```shell

# HTTP REQUEST OBJECT

{
	"AttachmentsIdList":
	[
		"5396b4d423aea51f4cbdab14",
		"5396b4d423aea51f4cbdab15",
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

This endpoint will get session id associated for a document type associated with an account.

This endpoint resembles a scenario when a recipient (client) click on document type of attachment to view.

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