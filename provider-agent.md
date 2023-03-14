# API Documentation

## URL

- <https://europe-west3-vesselticketing.cloudfunctions.net/bookingAPI>
- Request Method: POST
- Request Body Format: JSON (ApiRequest)
- Response Body Format: JSON (ApiResponse)
- Authorization Type: Basic Auth

## ApiRequest

```json
{
    "Action": "<Action Name>",
    "ProviderUID": "<string>",
    ...
}
```

## ApiResponse

```json
{
    "Data": <object>,         // if success
    "Error": "<description>", // if error
    "ErrorCode": <number>,    // if error
}
```

## Action: "Query Availabilities"

- Request:

```json
{
    "Action": "Query Availabilities",
    "ProviderUID": "<string>",
    "Day": "<string>" // Format: "YYYY-MM-DD"
}
```

- Response:

```json
{
    "Data" : {
        "Agent": {
            "UID": "<string>",
            "Name": "<string>",
        },
        "Buckets": {
            "UID": "<string>",
            "ScheduleUID": "<string>",
            "ScheduledTime": "<string>",
            "Cutoff": "<string>",
            "AddonMeal": <boolean>,
            "Prices": {
                "Age": <"Adult" | "Child" | "Infant">,
                "Price": <number>,
            }[],
            "Remaining": <number>,
            "Departure": {
                "UID": "<string>",
                "Day": "<string>",
                "Time": "<string>",
                "Ship": "<string>",
                "Remaining": <number>,
            }
        }[]
    }
}
```

## Action: "Query Bookings"

- Request:

```json
{
    "Action": "Query Bookings",
    "ProviderUID": "<ProviderUID>",
    "QueryDateBy": <"ScheduledDay" | "Created" | "Modified" | "Issued">,
    "DateFrom": "YYYY-MM-DD",
    "DateTo": "YYYY-MM-DD",
    "Limit": 100
}
```

- Response:

```json
{
    "Data" : { [UID: string]: Booking }
}
```

## Action: "Booking Create"

- Request:

```json
{
    "Action": "Booking Create",
    "ProviderUID": "<string>",
    "BucketUID": "<string>",
    "ScheduledDay": "<YYYY-MM-DD>",
    "DepartureUID": "<string?>",
    "PaymentMethod": "Credit",
    "IssueType": "B2B",
    "Name": "<string?>",
    "FirstName": "<string>",
    "LastName": "<string>",
    "Gender": "<string>",
    "Email": "<string?>",
    "Phone": "<string>",
    "Nationality": "",
    "Passengers": [
        {
            "Age": "Adult",
            "Type": "Guide",
            "Cost": 28
        },
        {
            "Age": "Child",
            "Cost": 14
        },
        {
            "Age": "Infant",
            "Cost": 0
        }
    ]
}
```

- Response:

```json
{
    "Data" : {
        "BookingUID": "<string>",
        "Passengers": (Passenger & { UID: string })[]
    }
}
```

## Action: "Booking Read"

- Request:

```json
{
    "Action": "Booking Read",
    "ProviderUID": "<string>",
    "BookingUID": "<string>"
}
```

- Response:

```json
{
    "Data" : {
        "Booking": {},
        "Passengers": []
    }
}
```

## Action: "Booking Update"

- Request:

```json
{
    "Action": "Booking Update",
    "ProviderUID": "<string>",
    "BookingUID": "<string>",
    "Booking": {
        "Name": "",
        "FirstName": "",
        "LastName": "",
        "Gender": "",
        "Email": "",
        "Phone": "",
        "Nationality": "",
        "Comments": ""
    }
}
```

- Response:

```json
{
    "Data" : "<timestamp>"
}
```

## Action: "Booking Disable"

- Request:

```json
{
    "Action": "Booking Disable",
    "ProviderUID": "<string>",
    "BookingUID": "<string>"
}
```

- Response:

```json
{
    "Data" : "<timestamp>"
}
```

## Action: "Booking Enable"

- Request:

```json
{
    "Action": "Booking Enable",
    "ProviderUID": "<string>",
    "BookingUID": "<string>"
}
```

- Response:

```json
{
    "Data" : "<timestamp>"
}
```

## Action: "Booking Boardings"

- Request:

```json
{
    "Action": "Booking Boardings",
    "ProviderUID": "<string>",
    "BookingUID": "<string>"
}
```

- Response:

```json
{
    "Data" : "<Base64_PDF>"
}
```

## Action: "Booking Receipt"

- Request:

```json
{
    "Action": "Booking Receipt",
    "ProviderUID": "<string>",
    "BookingUID": "<string>"
}
```

- Response:

```json
{
    "Data" : "<Base64_PDF>"
}
```

## Action: "Booking Resend"

- Request:

```json
{
    "Action": "Booking Resend",
    "ProviderUID": "<string>",
    "BookingUID": "<string>"
}
```

- Response:

```json
{
    "Data" : "<info>"
}
```

## Action: "Query Passengers"

- Request:

```json
{
    "Action": "Query Passengers",
    "ProviderUID": "<string>",
    "BookingUIDs": ["<string1>","<string2>",...]
}
```

- Response:

```json
{
    "Data" : <{ [bookingUID: string]: (Passenger & { UID: string })[] }>
}
```

## Action: "Passenger Create"

- Request:

```json
{
    "Action": "Passenger Create",
    "ProviderUID": "<string>",
    "BookingUID": "<string>",
    "Passengers": [
        {
            "Age": "Adult"
        }
    ]
}
```

- Response:

```json
{
    "Data" : <Passenger[]>
}
```

## Action: "Passenger Read"

- Request:

```json
{
    "Action": "Passenger Read",
    "ProviderUID": "<string>",
    "PassengerUID": "<string>"
}
```

- Response:

```json
{
    "Data" : <Passenger>
}
```

## Action: "Passenger Update"

- Request:

```json
{
    "Action": "Passenger Update",
    "ProviderUID": "<string>",
    "PassengerUID": "<string>"
    ...
}
```

- Response:

```json
{
    "Data" : "<timestamp>"
}
```

## Action: "Passenger Disable"

- Request:

```json
{
    "Action": "Passenger Disable",
    "ProviderUID": "<string>",
    "PassengerUID": "<string>"
}
```

- Response:

```json
{
    "Data" : <boolean>
}
```

## Action: "Passenger Enable"

- Request:

```json
{
    "Action": "Passenger Enable",
    "ProviderUID": "<string>",
    "PassengerUID": "<string>"
}
```

- Response:

```json
{
    "Data" : <boolean>
}
```

## Action: "Passenger Boarding"

- Request:

```json
{
    "Action": "Passenger Boarding",
    "ProviderUID": "<string>",
    "PassengerUID": "<string>"
}
```

- Response:

```json
{
    "Data" : "<Base64_PDF>"
}
```

## Action: "Passenger Resend"

- Request:

```json
{
    "Action": "Passenger Resend",
    "ProviderUID": "<string>",
    "PassengerUID": "<string>"
}
```

- Response:

```json
{
    "Data" : "<info>"
}
```
