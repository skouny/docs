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
    ...
}
```

- Response:

```json
{
    "Data" : <Object>
}
```

## Action: "Booking Read"

- Request:

```json
{
    "Action": "Booking Read",
    "ProviderUID": "<ProviderUID>",
    "BookingUID": "<BookingUID>"
}
```

- Response:

```json
{
    "Data" : <Object>
}
```

## Action: "Booking Update"

- Request:

```json
{
    "Action": "Booking Update",
    "ProviderUID": "<ProviderUID>",
    "BookingUID": "<BookingUID>",
    ...
}
```

- Response:

```json
{
    "Data" : <Object>
}
```

## Action: "Booking Disable"

- Request:

```json
{
    "Action": "Booking Disable",
    "ProviderUID": "<ProviderUID>",
    "BookingUID": "<BookingUID>"
}
```

- Response:

```json
{
    "Data" : <Object>
}
```

## Action: "Booking Enable"

- Request:

```json
{
    "Action": "Booking Enable",
    "ProviderUID": "<ProviderUID>",
    "BookingUID": "<BookingUID>"
}
```

- Response:

```json
{
    "Data" : <Object>
}
```

## Action: "Booking Boardings"

- Request:

```json
{
    "Action": "Booking Boardings",
    "ProviderUID": "<ProviderUID>",
    "BookingUID": "<BookingUID>"
}
```

- Response:

```json
{
    "Data" : <Object>
}
```

## Action: "Booking Receipt"

- Request:

```json
{
    "Action": "Booking Receipt",
    "ProviderUID": "<ProviderUID>",
    "BookingUID": "<BookingUID>"
}
```

- Response:

```json
{
    "Data" : <Object>
}
```

## Action: "Booking Resend"

- Request:

```json
{
    "Action": "Booking Resend",
    "ProviderUID": "<ProviderUID>",
    "BookingUID": "<BookingUID>"
}
```

- Response:

```json
{
    "Data" : <Object>
}
```

## Action: "Query Passengers"

- Request:

```json
{
    "Action": "Query Passengers",
    "ProviderUID": "<ProviderUID>",
    "BookingUIDs": <string[]>
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
    "Action": "<Action Name>",
    "ProviderUID": "<ProviderUID>",
    "BookingUID": "<BookingUID>",
    ...
}
```

- Response:

```json
{
    "Data" : <Object>
}
```

## Action: "Passenger Read"

- Request:

```json
{
    "Action": "<Action Name>",
    "ProviderUID": "<ProviderUID>",
    "PassengerUID": "<PassengerUID>"
}
```

- Response:

```json
{
    "Data" : <Object>
}
```

## Action: "Passenger Update"

- Request:

```json
{
    "Action": "<Action Name>",
    "ProviderUID": "<ProviderUID>",
    "PassengerUID": "<PassengerUID>"
    ...
}
```

- Response:

```json
{
    "Data" : <Object>
}
```

## Action: "Passenger Disable"

- Request:

```json
{
    "Action": "<Action Name>",
    "ProviderUID": "<ProviderUID>",
    "PassengerUID": "<PassengerUID>"
}
```

- Response:

```json
{
    "Data" : <Object>
}
```

## Action: "Passenger Enable"

- Request:

```json
{
    "Action": "<Action Name>",
    "ProviderUID": "<ProviderUID>",
    "PassengerUID": "<PassengerUID>"
}
```

- Response:

```json
{
    "Data" : <Object>
}
```

## Action: "Passenger Boarding"

- Request:

```json
{
    "Action": "<Action Name>",
    "ProviderUID": "<ProviderUID>",
    "PassengerUID": "<PassengerUID>"
}
```

- Response:

```json
{
    "Data" : <Object>
}
```

## Action: "Passenger Resend"

- Request:

```json
{
    "Action": "Passenger Resend",
    "ProviderUID": "<ProviderUID>",
    "PassengerUID": "<PassengerUID>"
}
```

- Response:

```json
{
    "Data" : <Object>
}
```
