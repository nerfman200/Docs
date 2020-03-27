[SimpleDateFormat]: https://docs.oracle.com/javase/7/docs/api/java/text/SimpleDateFormat.html
[link]: https://i.imgur.com/36aniDJ.png
[base-url]: https://purrbot.site/api

# PurrBotAPI
API used to create dynamic images based on the provided input.

!!! note "Base-URL"
    [https://purrbot.site/api][base-url]

!!! warning "Important"
    - All requests are performed through POST requests
	- The request body needs to contain valid JSON. Even when it is empty.

## /quote
*Generates images that look like Discord messages*

!!! note "Info"
    - Returns an image on success and JSON on failure.
	- All provided values need to be String.
	- Leave away a field and value to use the default option.

### Fields
| Field      | Description                                                                                                         | Default                                 |
| ---------- | ------------------------------------------------------------------------------------------------------------------- | --------------------------------------- |
| avatar     | The URL of the avatar to display.                                                                                   | [https://i.imgur.com/36aniDJ.png][link] |
| dateFormat | The format in which the date should be displayed. This uses the [SimpleDateFormat]                                  | `dd. MMM yyyy hh:mm:ss`                 |
| message    | The message itself to display. This __won't__ format markdown, emotes and only formats selected emojis.             | `Some message`                          |
| nameColor  | The color, in which the name should be displayed. You can provide `hex:rrggbb`, `rgb:r,g,b` or the raw color value. | `hex:ffffff`                            |
| timestamp  | The date and time as epoch milliseconds.                                                                            | `<Current time of the request>`         |
| username   | The name to display.                                                                                                | `Someone`                               |

!!! example
    **Request**  
    ```json
    {
      "avatar": "https://cdn.discordapp.com/avatars/204232208049766400/dfaaefa54a2804addb1f494da7aa904d.png",
      "message": "This is an example message.",
      "nameColor": "hex:ffffff",
	  "dateFormat": "dd. MMM yyyy",
      "username": "Andre_601"
    }
    ```
	
    **Result**  
	<img alt="quote" src="/assets/img/quote.png">

## /status
*Adds a status icon to the provided avatar*

!!! note "Info"
    - Returns an image on success and JSON on failure.
	- All provided values need to be String.
	- Leave away a field and value to use the default option.

### Fields
| Field      | Description                                                                                  | Default                                 |
| ---------- | -------------------------------------------------------------------------------------------- | --------------------------------------- |
| avatar     | The URL of the avatar to display.                                                            | [https://i.imgur.com/36aniDJ.png][link] |
| status     | The status to set as icon. Can be `online`, `idle`, `do_not_disturb` (or `dnd`) or `offline` | `offline`                               |

!!! example
    **Request**  
	```json
	{
	  "avatar": "https://cdn.discordapp.com/avatars/204232208049766400/dfaaefa54a2804addb1f494da7aa904d.png",
	  "status": "online"
	}
	```
	
	**Result**  
	<img alt="status" src="/assets/img/status.png" style="width: 80px; height: 80px;">

## Error responses
The API might return certain errors, depending on different facors.  
Possible errors are a `500 Internal Server Error` or a `403 Unauthorized Error`.

??? example "500 Internal Server Error"
    In the case of a `500 Internal Server Error` will you need to check the provided values as those may be invalid.  
	Common cause could be a image-link that is no longer valid.
	
    ```json
	{
	  "code": 500,
	  "message": "Couldn't generate image. Make sure the values are valid!"
	}
	```

??? example "403 Unauthorized Error"
    When a `403 Unauthorized Error` happens does it mean, that your provided JSON body is not valid.  
	This either means, that you didn't provide a valid JSON (i.e. a comma is missing) or you didn't provide any JSON at all.
	
    ```json
	{
	  "code": 403,
	  "message": "Invalid or empty JSON-body received!"
	}
	```