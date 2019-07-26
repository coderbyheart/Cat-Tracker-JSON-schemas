# JSON schema files for Cat Tracker application [Ongoing] :smirk_cat:

Contains the application protocol definition for the Cat Tracker application.

## Dynamic parameters and sensor data

```json
{
  "state": {
    "reported": {
      "bat": {
        "v": 2754,                       // Battery value as send from the modem
        "ts": "2019-07-24T11:45:47.123Z" // Timestamp with millisecond precision and timezone
      },
      "acc": {
          "v": [0.2, 0.777, 0],             // Accelerometor reading: x,y,z
          "ts": "2019-07-24T11:45:43.666Z" 
      },
      "gps": {
        "v": {
            "lng": 10.436642,
            "lat": 63.421133,
            "acc": 11,               // Accuracy
            "alt": 1234,             // Altitude
            "spd": 456,              // Speed
            "hdg": 176               // Heading
        },
        "ts": "2019-07-24T11:45:52.991Z"
      },
      "cfg": {
        "gpst": 720,               // GPS treshold (in seconds): timeout for GPS fix
        "act": false,              // Whether to enable the active mode
        "actwt": 60,               // In active mode: wait this amount of seconds until sending the next update. 
                                   //                 The actual interval will be this time plus the time it takes 
                                   //                 to get a GPS fix.
        "mvres": 60,               // (movement resolution) In passive mode: Time in seconds to wait after detecting movement
        "mvt": 3600,               // (movement timeout) In passive mode: Send update at least this often (in seconds)
        "acct": 12                 // (accelerometer threshold) absolute minimal value for and accelerometer reading to be considered movement as integer. 
                                   //                           Divide by 10 to get the real threshold.
                                   //                           Integers are used because the nRF9160 has issue parsing JSON floats. 
      }
    }
  }
}
```

## Tracking Modes

The device supports two tracking modes, active and passive. These modes are configurable via the mode JSON object. When mode is set to true, active mode is enabled and when mode is set to false, passive mode is enabled.

**Active Mode(mode = true):** In active mode the device publishes data every publishing interval.

**Passive Mode(mode=false):** In passive mode the device publishes data every publishing interval as long as the subject wearing the device is actually in movement. When the subject is for instance sleeping or standing still, the device will not publish data.
