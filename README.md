## Device

### GET `/api/v1/device/:mac`

Retrieve the designated room ID of a device.

`:mac` is the hypenated mac ID of the device, i.e.: `XX-XX-XX-XX-XX-XX`

#### → `200 OK`

```json
{
    "id": 5,
    "title": "Jupiter"
}
```

#### → `400 BAD REQUEST`

No device with `:mac` was found on DB.

```json
{
    "error": "Device unknown."
}
```

## Schedule

### GET `/api/v1/schedule/:id`

Retrieve the daily schedule of a given room.

`:id` is the room ID, obtained via device endpoint.

#### → `200 OK`

```json
[
    {
        "id": "h9u2f42ucfuse1chhovauobpdg",
        "title": "Daily Standup",
        "contact": "Batista Ford",
        "start": "2018-10-16T09:00:00+03:00",
        "end": "2018-10-16T10:00:00+03:00"
    },
    {
        "id": "60mntgpeuqq161cbp4d82aik1s",
        "title": "Project X Grooming",
        "contact": "Hank Kissinger",
        "start": "2018-10-16T10:00:00+03:00",
        "end": "2018-10-16T10:30:00+03:00"
    }
]
```

#### → `400 BAD REQUEST`

No room with `:id` was not found on DB.

```json
{
    "error": "Room unknown."
}
```

### POST `/api/v1/schedule/:id`

Post a booking for a given room.

| Payload | |
| ---: | :--- |
| `mins` | integer |

#### → `200 OK`

This response has no body.

#### → `400 BAD REQUEST`

Room may have been simulatenously booked on the calendar.

```json
{
    "error": "Room unavailable."
}
```