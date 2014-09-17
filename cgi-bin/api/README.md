AlephRx HTTP API
================

This is the documentation for a simple HTTP API to the AlephRx system. The
examples that follow assume that the [../](cgi-bin directory) is mapped to
`/alephrx/cgi-bin` on the server.

## Create a Report

POST XML to [reports](reports).

### Request

    POST /alephrx/cgi-bin/api/reports
    Content-Type: application/xml

    <report>
        <name>J. User</name>
        <functional_area>other</functional_area>
        <campus>UMCP</campus>
        <phone>301-555-0123</phone>
        <email>juser@example.com</email>
        <status>new</status>
        <summary>Problem Summary</summary>
        <text>Full text describing the issue...</text>
        <!-- submitter name is optional -->
        <submitter_name></submitter_name>
    </report>

### Responses

The `Content-Type` header for all responses is `text/plain`.

**200 OK** Report was created. The response body contains the URL of the newly
created report.

**400 Bad Request** Unable to parse the submitted data as XML, or there were
missing or invalid fields in the submitted data. If there are missing fields,
they are listed in the second paragraph of the response body.

**405 Method Not Allowed** A request method other than POST was used on this
endpoint.

**415 Unsupported Media Type** The request `Content-Type` header was set to
something other than `application/xml` (preferred) or `text/xml`.

**500 Internal Server Error** There was a problem creating the record in the
database.