# The OpenApi API


Prostore Open Api

This API has the following attributes:

| Attribute | Value                    |
|-----------|--------------------------|
| namespace | com.yahoo.prostore.oauth |
| version   | 1                        |


## Resources

### [Category](#Category)

#### GET /categories/{id}

Returns the category with the specified id.


#### Request parameters:

| Name   | Type   | Source        | Options  | Description                                                     |
|--------|--------|---------------|----------|-----------------------------------------------------------------|
| id     | Int64  | path          |          | the identity number of the category                             |
| fields | String | query: fields | optional | specified to retrieve partial fields, default return all fields |


#### Responses:

Expected:

| Code   | Type     |
|--------|----------|
| 200 OK | Category |


Exception:

| Code                      | Type          | Comment                      |
|---------------------------|---------------|------------------------------|
| 400 Bad Request           | ResourceError | if the input data is invalid |
| 401 Unauthorized          | ResourceError | if not authenticated         |
| 403 Forbidden             | ResourceError | if not authorized            |
| 404 Not Found             | ResourceError | if the id already exists     |
| 500 Internal Server Error | ResourceError | if internal server error     |


### [Categories](#Categories)

#### GET /categories

Returns multiple Categories with the specified ids.


#### Request parameters:

| Name   | Type   | Source        | Options  | Description                                                     |
|--------|--------|---------------|----------|-----------------------------------------------------------------|
| ids    | String | query: ids    |          | the identity number of the category                             |
| fields | String | query: fields | optional | specified to retrieve partial fields, default return all fields |


#### Responses:

Expected:

| Code   | Type       |
|--------|------------|
| 200 OK | Categories |


Exception:

| Code                      | Type          | Comment                      |
|---------------------------|---------------|------------------------------|
| 400 Bad Request           | ResourceError | if the input data is invalid |
| 401 Unauthorized          | ResourceError | if not authenticated         |
| 403 Forbidden             | ResourceError | if not authorized            |
| 404 Not Found             | ResourceError | if the id already exists     |
| 500 Internal Server Error | ResourceError | if internal server error     |


#### GET /categories/{id}/parents

Return parent Categories with the specified ids.


#### Request parameters:

| Name   | Type   | Source        | Options  | Description                                                     |
|--------|--------|---------------|----------|-----------------------------------------------------------------|
| id     | Int64  | path          |          | the identity number of the category                             |
| fields | String | query: fields | optional | specified to retrieve partial fields, default return all fields |


#### Responses:

Expected:

| Code   | Type       |
|--------|------------|
| 200 OK | Categories |


Exception:

| Code                      | Type          | Comment                      |
|---------------------------|---------------|------------------------------|
| 400 Bad Request           | ResourceError | if the input data is invalid |
| 401 Unauthorized          | ResourceError | if not authenticated         |
| 403 Forbidden             | ResourceError | if not authorized            |
| 404 Not Found             | ResourceError | if the id already exists     |
| 500 Internal Server Error | ResourceError | if internal server error     |


#### GET /categories/{id}/descendants/{depth}

Returns descendants Categories with the specified ids.


#### Request parameters:

| Name   | Type   | Source        | Options   | Description                                                     |
|--------|--------|---------------|-----------|-----------------------------------------------------------------|
| id     | Int64  | path          |           | the identity number of the category                             |
| depth  | Int32  | path          | default=1 | specified level of descendant to be returned 0 = all; 1 = self; |
| fields | String | query: fields | optional  | specified to retrieve partial fields, default return all fields |


#### Responses:

Expected:

| Code   | Type       |
|--------|------------|
| 200 OK | Categories |


Exception:

| Code                      | Type          | Comment                      |
|---------------------------|---------------|------------------------------|
| 400 Bad Request           | ResourceError | if the input data is invalid |
| 401 Unauthorized          | ResourceError | if not authenticated         |
| 403 Forbidden             | ResourceError | if not authorized            |
| 404 Not Found             | ResourceError | if the id already exists     |
| 500 Internal Server Error | ResourceError | if internal server error     |


## Types

### <a name="ParsecErrorDetail"></a> ParsecErrorDetail

DO NOT MODIFY This file is for who want to use ParsecResourceError as error
layout. But the structure here is only a reminder for user. It will not be
parsed by Parsec. Change this file will not affect the implementation of
ParsecResourceError. If you want to change the error layout of api end point,
you can customize your own error layout class.

`ParsecErrorDetail` is a `Struct` type with the following fields:

| Name         | Type   | Options | Description | Notes |
|--------------|--------|---------|-------------|-------|
| message      | String |         |             |       |
| invalidValue | String |         |             |       |


### <a name="ParsecErrorBody"></a> ParsecErrorBody

Parsec error response entity object

`ParsecErrorBody` is a `Struct` type with the following fields:

| Name    | Type                                                 | Options | Description   | Notes |
|---------|------------------------------------------------------|---------|---------------|-------|
| code    | Int32                                                |         | error code    |       |
| message | String                                               |         | error message |       |
| detail  | Array&lt;[ParsecErrorDetail](#parsecerrordetail)&gt; |         | error detail  |       |


### <a name="ParsecResourceError"></a> ParsecResourceError

This error model is designed for following EC REST API Convention (yo/ecrest)

`ParsecResourceError` is a `Struct` type with the following fields:

| Name  | Type                                | Options | Description  | Notes |
|-------|-------------------------------------|---------|--------------|-------|
| error | [ParsecErrorBody](#parsecerrorbody) |         | error object |       |


### <a name="CategoryAttribute"></a> CategoryAttribute

A category attribute instance.

`CategoryAttribute` is a `Struct` type with the following fields:

| Name  | Type   | Options | Description                          | Notes |
|-------|--------|---------|--------------------------------------|-------|
| name  | String |         | the name of the category attribute.  |       |
| value | String |         | the value of the category attribute. |       |


### <a name="Category"></a> Category

A category instance (e.g., 電腦/週邊).

`Category` is a `Struct` type with the following fields:

| Name           | Type                                                 | Options | Description                                                    | Notes |
|----------------|------------------------------------------------------|---------|----------------------------------------------------------------|-------|
| id             | Int64                                                |         | the identity number of the category                            |       |
| name           | String                                               |         | the name of the category.                                      |       |
| path           | String                                               |         | the breadcrumb path to the category.                           |       |
| level          | Int32                                                |         | the level of the category in the whole category tree.          |       |
| isLink         | Bool                                                 |         | if the category is alias of another category.                  |       |
| isLeaf         | Bool                                                 |         | if the category is the last level of the category path.        |       |
| parentId       | Int64                                                |         | the identity number of the parent category                     |       |
| custAttributes | Array&lt;[CategoryAttribute](#categoryattribute)&gt; |         | A list of [CategoryAttribute](objects.html#CategoryAttribute). |       |


### <a name="Categories"></a> Categories
`Categories` is a `Struct` type with the following fields:

| Name         | Type                               | Options | Description                                                                                                                                       | Notes |
|--------------|------------------------------------|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|-------|
| categories   | Array&lt;[Category](#category)&gt; |         | A list of [Category](objects.html#Category).                                                                                                      |       |
| resultsTotal | Int32                              |         | The total number of items in all the pages.                                                                                                       |       |
| nextOffset   | Int32                              |         | If there are more items yet to be returned, this value will be present and can be used in the offset parameter to retrieve the next set of items. |       |

