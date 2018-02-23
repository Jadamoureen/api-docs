# Accounts

## Introduction

Accounts hold your funds. The accounts api method allows you to list your accounts and view balances for each account. When you sign up for Beyonic, at least one account in your primary currency is created for your organization. You can request additional accounts if needed.

The accounts api endpoint is:

    <aside class="notice">https://app.beyonic.com/api/accounts</aside>

## The Account object

> Sample Account Object (JSON):

```json
{
    "id": 1146,
    "organization":1,
    "balance": 200.0,
    "currency": "KES",
    "status": "active",
    "created": "2015-02-13T04:22:31Z",
    "author": 7,
    "modified": "2015-02-26T13:00:35Z",
    "updated_by": 1
}
```

Field | Type | Description
----- | -----| ----
id | long integer | Unique object identifier
organization | long integer | The ID of the organization that the account belongs to. (This is usually your organization ID)
balance | float | The current account balance
currency | string | The account's currency code. i.e KES, UGX
status | string | The account's status. One of: active or inactive
created | string | The date that the account was created, in the UTC timezone. Format: "YYYY-MM-DDTHH:MM:SSZ"
author | long integer | The ID of the user who created the account
modified | string | The date that the account was last modified, in the UTC timezone. Format: "YYYY-MM-DDTHH:MM:SSZ"
updated_by | string | The ID of the user who last updated the account

## Retrieving a Single Account

> Sample Request:

```shell
curl https://app.beyonic.com/api/accounts/12 -H "Authorization: Token ab594c14986612f6167a975e1c369e71edab6900"
```

```ruby
require 'beyonic'
Beyonic.api_key = 'ab594c14986612f6167a975e1c369e71edab6900'

account = Beyonic::Account.get(12)
```

```php
<?php
require_once('./lib/Beyonic.php');
Beyonic::setApiKey("ab594c14986612f6167a975e1c369e71edab6900");

$account = Beyonic_Account::get(12);
?>
```

```python
import beyonic
beyonic.api_key = 'ab594c14986612f6167a975e1c369e71edab6900'

account = beyonic.Account.get(12)
```

```java
package com.beyonic.examples.account;

import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;


public class SingleAccountExample {

    private static final String API_ENDPOINT = "https://app.beyonic.com/api/accounts";
    private static final String API_KEY = "ab594c14986612f6167a975e1c369e71edab6900";
    private static final String CHARSET = "UTF-8";

    public static void main(String[] args){
        URL url = null;
        try {
            url = new URL(API_ENDPOINT + "/12");
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();

            conn.setRequestProperty("Content-Type", "application/json");
            conn.setRequestProperty("Accept", "application/json");
            conn.setRequestProperty("charset", CHARSET);
            conn.setRequestProperty("Authorization", "Token " + API_KEY);

            System.out.println(conn.getResponseCode() + " // " + conn.getResponseMessage());

            try {
                if (conn.getResponseCode() == 200) {
                    InputStream inputStream = conn.getInputStream();
                    BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
                    String response = reader.readLine();
                    reader.close();

                    System.out.println(response);
                }
            } finally {
                conn.disconnect();
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

> Sample Response (JSON) - if you use one of the development libraries, this is automatically converted into a native object for you:

```json
{
    "id": 12,
    "organization":1,
    "balance": 200.0,
    "currency": "KES",
    "status": "active",
    "created": "2015-02-13T04:22:31Z",
    "author": 7,
    "modified": "2015-02-26T13:00:35Z",
    "updated_by": 1
}
```

To retrieve a single account, provide the account id and a account object will be returned.

Parameter | Required | Type | Example | Notes
--------- | -------- | ---- | ------- | -----
id | Yes | Integer | 12 | The id of the account you want to retrieve

## Listing all accounts

> Sample Request:

```shell
curl https://app.beyonic.com/api/accounts -H "Authorization: Token ab594c14986612f6167a975e1c369e71edab6900"
```

```ruby
require 'beyonic'
Beyonic.api_key = 'ab594c14986612f6167a975e1c369e71edab6900'

accounts = Beyonic::Account.list
```

```php
<?php
require_once('./lib/Beyonic.php');
Beyonic::setApiKey("ab594c14986612f6167a975e1c369e71edab6900");

$accounts = Beyonic_Account::getAll();
?>
```

```python
import beyonic
beyonic.api_key = 'ab594c14986612f6167a975e1c369e71edab6900'

accounts = beyonic.Account.list()

```

```java
package com.beyonic.examples.accounts;

import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class ListAllAccountsExample {

    private static final String API_ENDPOINT = "https://app.beyonic.com/api/accounts";
    private static final String API_KEY = "ab594c14986612f6167a975e1c369e71edab6900";
    private static final String CHARSET = "UTF-8";

    public static void main(String[] args){
        URL url = null;
        try {
            url = new URL(API_ENDPOINT);
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();

            conn.setRequestProperty("Content-Type", "application/json");
            conn.setRequestProperty("Accept", "application/json");
            conn.setRequestProperty("charset", CHARSET);
            conn.setRequestProperty("Authorization", "Token " + API_KEY);

            System.out.println(conn.getResponseCode() + " // " + conn.getResponseMessage());

            try {
                if (conn.getResponseCode() == 200) {
                    InputStream inputStream = conn.getInputStream();
                    BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
                    String response = reader.readLine();
                    reader.close();

                    System.out.println(response);
                }
            } finally {
                conn.disconnect();
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

> Sample Response (JSON)  - if you use one of the development libraries, this is automatically converted into a native object for you:

```json
{
    "count": 2,
    "next": "https://app.beyonic.com/api/accounts?offset=10",
    "previous": null,
    "results": [
        {
            "id": 1146,
            "organization":1,
            "balance": 200.0,
            "currency": "KES",
            "status": "active",
            "created": "2015-02-13T04:22:31Z",
            "author": 7,
            "modified": "2015-02-26T13:00:35Z",
            "updated_by": 1
        },
        {
            "id": 1147,
            "organization":1,
            "balance": 100.0,
            "currency": "UGX",
            "status": "active",
            "created": "2015-02-13T04:22:31Z",
            "author": 7,
            "modified": "2015-02-26T13:00:35Z",
            "updated_by": 1
        },
    ]
}
```

To retrieve a list of all accounts, make a GET request to the accounts end point. This will return a list of accounts.

## Filtering Accounts

> Sample Request:

```shell
curl https://app.beyonic.com/api/accounts?currency=KES -H "Authorization: Token ab594c14986612f6167a975e1c369e71edab6900"
```

```ruby
require 'beyonic'
Beyonic.api_key = 'ab594c14986612f6167a975e1c369e71edab6900'

accounts = Beyonic::Account.list(
  currency: "KES"
)
```

```php
<?php
require_once('./lib/Beyonic.php');
Beyonic::setApiKey("ab594c14986612f6167a975e1c369e71edab6900");

$accounts = Beyonic_Account::getAll(array(
  "currency" => "KES"
));
?>
```

```python
import beyonic
beyonic.api_key = 'ab594c14986612f6167a975e1c369e71edab6900'

accounts = beyonic.Account.list(currency='KES')

```

```java
package com.beyonic.examples.accounts;

import java.io.BufferedReader;
import java.io.InputStream;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class FilterAccountsExample {

    private static final String API_ENDPOINT = "https://app.beyonic.com/api/accounts";
    private static final String API_KEY = "ab594c14986612f6167a975e1c369e71edab6900";
    private static final String CHARSET = "UTF-8";

    public static void main(String[] args){
        URL url = null;
        try {
            url = new URL(API_ENDPOINT + "?currency=UGX");
            HttpURLConnection conn = (HttpURLConnection) url.openConnection();

            conn.setRequestProperty("Content-Type", "application/json");
            conn.setRequestProperty("Accept", "application/json");
            conn.setRequestProperty("charset", CHARSET);
            conn.setRequestProperty("Authorization", "Token " + API_KEY);

            System.out.println(conn.getResponseCode() + " // " + conn.getResponseMessage());

            try {
                if (conn.getResponseCode() == 200) {
                    InputStream inputStream = conn.getInputStream();
                    BufferedReader reader = new BufferedReader(new InputStreamReader(inputStream));
                    String response = reader.readLine();
                    reader.close();

                    System.out.println(response);
                }
            } finally {
                conn.disconnect();
            }

        } catch (Exception e) {
            e.printStackTrace();
        }
    }

}
```

You can search or filter accounts on the following fields. Simply add them to your request as shown in the examples. You can combine multiple filters. Note that filters return exact matches only.

* currrency - the account currency
* status - the account status
* created_after - only return accounts created after this date (E.g. 2017-01-01 00:00)
* created_before - only return accounts created before this date (E.g. 2017-01-01 00:00)