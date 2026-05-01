Now many web applications rely on APIs. Instead of using PHP parameters to search for a city, API can be used to achieve same.

## APIs
Several types of APIs available. They are used to interact with database tables as shown in the below example `api.php` , we want to update a table name `city` and the row we will be updating has city name `london`

```
curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london ...SNIP...
```

## CRUD
There are 4 operations performed on entities inside database:

|Operation|HTTP Method|Description|
|---|---|---|
|`Create`|`POST`|Adds the specified data to the database table|
|`Read`|`GET`|Reads the specified entity from the database table|
|`Update`|`PUT`|Updates the data of the specified database table|
|`Delete`|`DELETE`|Removes the specified row from the database table|
These are commonly known as CRUD Apis.

## Read
This allow client to read data from the database. HTTP method used for this is GET

```
aliyark145@htb[/htb]$ curl http://<SERVER_IP>:<PORT>/api.php/city/london

[{"city_name":"London","country_name":"(UK)"}]
```

the result is returned as JSON string. To properly format it in JSON, we can use a tool called jq.

```
aliyark145@htb[/htb]$ curl -s http://<SERVER_IP>:<PORT>/api.php/city/london | jq 
[ 
	{ 
		"city_name": "London", 
		"country_name": "(UK)" 
	} 
]
```

`-s` is used to silent any unneeded logs from cURL.

we can pass a search term or empty string to retrieve matching or all items for that table.

## Create
To add a new entry to the table, we can use HTTP post method to add a new entry by sending data as JSON and a header `Content-Type` set to `application/json`.

```
aliyark145@htb[/htb]$ curl -X POST http://<SERVER_IP>:<PORT>/api.php/city/ -d '{"city_name":"HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'
```

We can retrieve the city to make sure it has been added in the table by sending the Read request

```
aliyark145@htb[/htb]$ curl -s http://<SERVER_IP>:<PORT>/api.php/city/HTB_City | jq

[
  {
    "city_name": "HTB_City",
    "country_name": "HTB"
  }
]
```

## Update
To update a record, we can use the HTTP PUT method to update the record with a new record.

```
aliyark145@htb[/htb]$ curl -X PUT http://<SERVER_IP>:<PORT>/api.php/city/london -d '{"city_name":"New_HTB_City", "country_name":"HTB"}' -H 'Content-Type: application/json'
```

```
aliyark145@htb[/htb]$ curl -s http://<SERVER_IP>:<PORT>/api.php/city/HTB_City | jq

[
  {
    "city_name": "HTB_City",
    "country_name": "HTB"
  }
]

```

Indeed we updated the record by using the PUT

**Note** We can also use PATCH. The difference is PUT is used to update a full record, while PATCH is used to update partial record

## DELETE
To delete a record we can use, HTTP Delete method as follows:

```
aliyark145@htb[/htb]$ curl -X DELETE http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City
```

```
aliyark145@htb[/htb]$ curl -s http://<SERVER_IP>:<PORT>/api.php/city/New_HTB_City | jq 

[]
```

The empty array denotes that there is no matching record. Proving record has been deleted.