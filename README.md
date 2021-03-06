## discord.js docs API

A simple API to serve discord.js docs using [discord.js-docs](https://github.com/TeeSeal/discord.js-docs).

## Routes

### GET `/:project/:branch`
Returns the entire formatted documentation for the given project and branch.\
Project can be one of: `main`, `commando`, `rpc`.

> Set the `raw` queryparam to `true` to receive the original fetched JSON without any formatting.\
> Doesn't work for the `/search` and `/embed` endpoints.\
> Example: `/main/master?raw=true`, `/main/stable/message/content?raw=true`

> Set the `force` queryparam to `true` to force fetch the docs instead of reading from cache.\
> Works for all endpoints.\
> Example: `/main/master?force=true`

### GET `/:project/:branch/el/:parent/:child`
Returns the documentation for a single element.\
`:parent` and `:child` have to be element names. Case does not matter.\
`:child` can be omitted.

### GET `/:project/:branch/search`
Searches the documentation using fuzzy search and returns top 10 hits.\
The query must be specified under the `q` queryparam.

Will return 400 if no query specified.

Example:
```
/main/master/search?q=reaction%20collector
```

### GET `/:project/:branch/embed`
Tries to resolve the query into a single element.\
The query must be specified under the `q` queryparam.\
If that fails, falls back to the behaviour of the `.../search` route.\
Query is expected to be separated with `#` (%23 when uri encoded) or `.` for exact searches.

The result is formatted into a [Discord embed object](https://discordapp.com/developers/docs/resources/channel#embed-object).

Will return 400 if no query specified.

Examples:
```
/main/stable/embed?q=message%23pin
/main/master/embed?q=reaction%20collector
```
