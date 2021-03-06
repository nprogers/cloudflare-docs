# Require specific HTTP headers

<Aside type='warning'>

Access to HTTP header and body fields require a Cloudflare Enterprise plan.

</Aside>

Many organizations qualify traffic based on the presence of specific HTTP request headers.

Use the Firewall Rules [HTTP header and body fields](/cf-firewall-language/fields/#http-header-and-body-fields) to target requests with specific headers.

This example uses the `http.headers.names` field to look for the presence of an X-CSRF-Token header. The `lower()` [transformation function](/cf-firewall-language/functions/#transformation-functions) converts the value to lowercase so that the expression is case insensitive.

When the X-CSRF-Token header is missing, Cloudflare blocks the request.

<TableWrap>

| Expression                                                                                                                                   | Action |
| -------------------------------------------------------------------------------------------------------------------------------------------- | ------ |
| `not any(lower(http.request.headers.names[*])[*] contains "x-csrf-token") and (http.request.full_uri eq "https://www.example.com/somepath")` | Block  |

</TableWrap>
