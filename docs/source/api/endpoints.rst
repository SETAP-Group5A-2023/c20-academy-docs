Endpoints
=========

All endpoints are relative to the API's domain name, in the case of the official API, :code:`api.c20.academy`.
Each endpoint corresponds to a single data type, and parameters should be passed as URL-encoded query parameters, e.g. :code:`/v1/article?id=1`.

.. note::

  All endpoints are currently at version 1, but this may change in the future. If an endpoint stops responding, check back here in case there is a new version.

/v1/article
-----------

Returns a single article from the database, as per it's ID.

.. list-table:: Arguments
  :header-rows: 0

  * - | :code:`id`
      | REQUIRED
    - A positive integer representing the ID of an article in the database

.. list-table:: Return Values
  :header-rows: 0

  * - | :code:`generatedAt`
      | REQUIRED
    - An ISO 8601 formatted timestamp representing when the response was generated by the server
  * - | :code:`result`
      | OPTIONAL
    - Contains :code:`null` if the ID is invalid or not found, otherwise the values from the database corresponding to the ID of the request
  * - | :code:`result.id`
      | REQUIRED
    - The database ID of the article
  * - | :code:`result.title`
      | REQUIRED
    - The title of the article, which should be displayed at the top of the article
  * - | :code:`result.date`
      | REQUIRED
    - The date the article was published to the API
  * - | :code:`result.scripture`
      | REQUIRED
    - The actual main text of the article, in Markdown
  * - | :code:`result.references`
      | REQUIRED
    - An array of references for the content of the article

Example
+++++++

Request::

  /v1/article?id=1

Returns::

  {
    "generatedAt": "2024-03-17T15:22:30.608065",
    "result": {
      "id": 1,
      "title": "Irish War of Independence",
      "date": "2024-03-11T00:00:00.000Z",
      "scripture": "Dummy Text",
      "references": [
        {
          "id": 1,
          "author": "John Smith",
          "title": "The Irish War of Independence and it's consequences",
          "publication_date": "1990-01-01T00:00:00.000Z",
          "url": null,
        }
      ]
    }
  }

/v1/article/search
-----------

Returns a list of articles which match the search term

.. list-table:: Arguments
  :header-rows: 0

  * - | :code:`q`
      | REQUIRED
    - A search term which article titles should be matched against

.. list-table:: Return Values
  :header-rows: 0

  * - | :code:`generatedAt`
      | REQUIRED
    - An ISO 8601 formatted timestamp representing when the response was generated by the server
  * - | :code:`results`
      | REQUIRED
    - An array of articles which match the search term
  * - | :code:`results[].id`
      | REQUIRED
    - The database ID of the article, which can be used with other endpoints
  * - | :code:`results[].title`
      | REQUIRED
    - The title of the article, which matched the search term
  * - | :code:`results[].date`
      | REQUIRED
    - The date the article was published to the API

Example
+++++++

Request::

  /v1/article/search?q=Irish

Returns::

  {
    "generatedAt": "2024-03-17T16:02:22.271464",
    "results": [
      {
        "id": 1,
        "title": "Irish War of Independence",
        "date": "2024-03-11T00:00:00.000Z"
      }
    ]
  }

/v1/country
-----------

Returns a single country from the database, as per it's ID.

.. list-table:: Arguments
  :header-rows: 0

  * - | :code:`id`
      | REQUIRED
    - A positive integer representing the ID of a country in the database

.. list-table:: Return Values
  :header-rows: 0

  * - | :code:`generatedAt`
      | REQUIRED
    - An ISO 8601 formatted timestamp representing when the response was generated by the server
  * - | :code:`result`
      | OPTIONAL
    - Contains :code:`null` if the ID is invalid or not found, otherwise the values from the database corresponding to the ID of the request
  * - | :code:`result.id`
      | REQUIRED
    - The database ID of the country
  * - | :code:`result.dateEst`
      | REQUIRED
    - The date the country is said to be established
  * - | :code:`result.currentName`
      | REQUIRED
    - The current name of the country
  * - | :code:`result.names`
      | REQUIRED
    - An array of previous names for the country
  * - | :code:`result.populations`
      | REQUIRED
    - An array of approximate populations for the country
  * - | :code:`result.articles`
      | REQUIRED
    - An array of articles related to the country
  * - | :code:`result.triviaSections`
      |
    - An array of trivia sections related to the country

Example
+++++++

Request::

  /v1/country?id=1

Response::

  {
    "generatedAt": "2024-03-18T11:38:07.656825",
    "result": {
      "id": 2,
      "dateEst": "1922-12-06T00:00:00.000Z",
      "currentName": {
        "id": 4,
        "name": "The Republic of Ireland (Éire)",
        "startDate": "1948-12-02T00:00:00.000Z",
        "endDate": "3000-01-01T00:00:00.000Z"
      },
      "names": [
        {
          "id": 5,
          "name": "Ireland (Éire)",
          "startDate": "1937-12-29T00:00:00.000Z",
          "endDate": "1948-12-01T00:00:00.000Z"
        },
        {
          "id": 6,
          "name": "The Irish Free State (Saorstát Éireann)",
          "startDate": "1922-12-06T00:00:00.000Z",
          "endDate": "1937-12-28T00:00:00.000Z"
        }
      ],
      "populations": [
        {
          "id": 13,
          "approxPopulation": 3100000,
          "date": "1920-01-01T00:00:00.000Z"
        }
      ],
      "articles": [
        {
          "id": 1,
          "title": "Irish War of Independence",
          "date": "2024-03-11T00:00:00.000Z"
        }
      ],
      "triviaSections": []
    }
  }

/v1/country/search
------------------

.. list-table:: Arguments
  :header-rows: 0

  * - | :code:`q`
      | REQUIRED
    - A search term which country names (current and previous) should be matched against

.. list-table:: Return Values
  :header-rows: 0

  * - | :code:`generatedAt`
      | REQUIRED
    - An ISO 8601 formatted timestamp representing when the response was generated by the server
  * - | :code:`results`
      | REQUIRED
    - An array of countries which match the search term
  * - | :code:`results[].id`
      | REQUIRED
    - The database ID of the country, which can be used with other endpoints
  * - | :code:`results[].currentName`
      | REQUIRED
    - The current name of the country
  * - | :code:`results[].names`
      | REQUIRED
    - An array of previous names for the country, which may have matched the search term

Example
+++++++

Request::

  /v1/country/search?q=the

Response::

  {
    "generatedAt": "2024-03-18T11:38:56.829440",
    "results": [
      {
        "id": 1,
        "dateEst": "1535-01-01T00:00:00.000Z",
        "currentName": {
          "id": 1,
          "name": "The United Kingdom of Great Britain and Northern Ireland",
          "startDate": "1927-04-12T00:00:00.000Z",
          "endDate": "3000-01-01T00:00:00.000Z"
        },
        "names": [
          {
            "id": 2,
            "name": "The United Kingdom of Great Britain and Ireland",
            "startDate": "1801-01-01T00:00:00.000Z",
            "endDate": "1927-04-11T00:00:00.000Z"
          },
          {
            "id": 3,
            "name": "The Kingdom of Great Britain",
            "startDate": "1707-01-01T00:00:00.000Z",
            "endDate": "1800-12-31T00:00:00.000Z"
          }
        ]
      },
      {
        "id": 2,
        "dateEst": "1922-12-06T00:00:00.000Z",
        "currentName": {
          "id": 4,
          "name": "The Republic of Ireland (Éire)",
          "startDate": "1948-12-02T00:00:00.000Z",
          "endDate": "3000-01-01T00:00:00.000Z"
        },
        "names": [
          {
            "id": 5,
            "name": "Ireland (Éire)",
            "startDate": "1937-12-29T00:00:00.000Z",
            "endDate": "1948-12-01T00:00:00.000Z"
          },
          {
            "id": 6,
            "name": "The Irish Free State (Saorstát Éireann)",
            "startDate": "1922-12-06T00:00:00.000Z",
            "endDate": "1937-12-28T00:00:00.000Z"
          }
        ]
      }
    ]
  }