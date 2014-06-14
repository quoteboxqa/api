# Team Member

## Invite

This endpoint will send an invitation via email to join Quotebox.

This endpoint resembles a scenario when a user wants to invite another user to his/her account on Quotebox.

```shell
# HTTP REQUEST BODY

{
	"email":"jane@company.com", 
	"phonenumber":"012345678", 
	"firstname":"jane", 
	"lastname":"doe",
	"timezone":"+5:30 GMT",
	"isadmin":false,
	"accountname":"GolboMantics Corp"
}
```

### HTTP REQUEST

`POST api/Account/Invite`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST BODY PARAMETERS

Parameter | Description
-------------- | --------------
firstname | **required** <i>- 3 to 25 characters long</i> <br> first name of the user
lastname | **required** <i>- 3 to 25 characters long</i> <br> last name of the user
email | **required** <i>- 10 to 65 characters long</i> <br> email of the user
phonenumber | **optional** <i>- only digits allowed </i> <br> phone number of the user
isadmin | **optional** ***- boolean***<i>, false by default </i> <br> true if the intended user is an administrator for the associated account
accountname | **optional** <br> name of the account to invite the user in Quotebox

### HTTP RESPONSE

<aside class="success">
200 OK
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>

## Get

This endpoint will get the details of a invited team member.

This endpoint resembles as scenario when a user wants to get invited team member related meta data.

```shell
# HTTP REQUEST BODY

{
	"invitekey":"2270912302132140681661241340940041440111312381670 ... "
}
```

> The above request should return the following JSON

```shell

{
	"TeamMemberId":"539ac7b523aea51bbc10dcbf",
	"Email":"jhon@papa.com",
	"PhoneNumber":null,
	"FirstName":"Test",
	"LastName":"Sample",
	"UserType":true,
	"AccountName":"",
	"AccountId":"539ac73523aea51bbc10dcbb",
	"Errors":[]
}

```

### HTTP REQUEST

`POST api/Account/InvitedTeamMember`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST BODY PARAMETERS

Parameter | Description
-------------- | --------------
invitekey | **required** <br> invitation key to get details of invited team member (available via invitation link sent as email to the invited user)

### HTTP RESPONSE

<aside class="success">
200 OK
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>

## Delete

This endpoint will delete an invitation.

Should you prevent a user from joining your account once invited, make a call to this endpoint to delete invitation for a user.

```shell
# HTTP REQUEST BODY

{
	"teammemberid":"5380700d995ba3047cc5ff1c"
}
```

### HTTP REQUEST

`POST api/Account/DeleteInvite`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST BODY PARAMETERS

Parameter | Description
-------------- | --------------
teammemberid | **required** <br> id of team member to delete invitation for

### HTTP RESPONSE

<aside class="success">
200 OK
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>

## Accept

This endpoint will accept the invitation to join an account with Quotebox.

This endpoint resembles a scenario when an invited user wants to accept the invitation to join Quotebox.

```shell
# HTTP REQUEST BODY

{
	"invitekey":"2270912302132140681661241340940041440111312381670 ... ",
	"password":"P@ssw0rd",
	"confirmpassword":"P@ssw0rd"
}
```

### HTTP REQUEST

`POST api/Account/AcceptInvite`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST BODY PARAMETERS

Parameter | Description
-------------- | --------------
password | **required** <i>- 8 to 16 characters long</i> <br> password required to authorize login
confirmpassword | **required** <i>- 8 to 16 characters long</i> <br> retype password required to authorize login
invitekey | **required** <br> invitation key required to verify the invitation request (available from link sent via email of invitation sent to the user)

### HTTP RESPONSE

<aside class="success">
200 OK
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>

## List

This endpoint will list amongst team member(s).

This endpoint resembles a scenario when an user wants to list associated team members.

> The list request should return following JSON

```shell
# HTTP RESPOSNE OBJECT

{
	"TeamMembers": 
	[ 
		{ 
			"id":"5380700d995ba3047cc5ff1c", 
			"email":"jane@company.com", 
			"firstname":"jane", 
			"lastname":"john", 
			"isadmin":false, 
			"fullname":"jane doe", 
			"expireson":"05/09/2020 10:10 AM" 
		} ... 
	]
}
```

### HTTP REQUEST

`POST api/Account/List`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP RESPONSE

<aside class="success">
200 OK
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>

## Remove

This endpoint will remove a team member from associated account.

Should you remove a team member (de-associate) associated with your account, make a call to this endpoint.

**Note:** This action would de-active the user (team member) you removed and there after he/she will have to sign-up again with different email to continue using Quotebox.

```shell
# HTTP REQUEST BODY

{
	"teammemberid":"5380700d995ba3047cc5ff1c"
}
```

### HTTP REQUEST

`POST api/Account/RemoveTeamMember`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST BODY PARAMETERS

Parameter | Description
-------------- | --------------
teammemberid | **required** <br> id of team member to be removed

### HTTP RESPONSE

<aside class="success">
200 OK 
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>

## Update

This endpoint will update alternate email and rights for a team member associated with an account.

This endpoint resembles a scenario when a user wants to update meta data for an associated team member such as ***alternate email*** and/or ***rights*** - <i>admin or user</i>

```shell
# HTTP REQUEST BODY

{
	"teammemberid":"5380700d995ba3047cc5ff1c",
	"isadmin":true,
	"alternateemail":"john@company.com"
}
```

### HTTP REQUEST

`POST api/Account/UpdateTeamMember`

<aside class="notice">
Include bearer token in header to authorize: `Authorization: Bearer token_value`
</aside>

### HTTP REQUEST BODY PARAMETERS

Parameter | Description
-------------- | --------------
teammemberid | **required** <br> id of team member to update
isadmin | **optional** ***- boolean***<i>, false by default </i> <br> true if the intended user is an administrator for the associated account
alternateemail | **optional** <br> alternate email of team member

### HTTP RESPONSE

<aside class="success">
200 OK 
</aside>

<aside class="warning">
400 Badrequest - { validation related errors }
</aside>