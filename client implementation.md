# Conditional GET Client implementation (HTTP/1.1) #

```http
GET /home.html HTTP/1.1
Host: developer.mozilla.org
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate, br
Referer: https://developer.mozilla.org/testpage.html
Connection: keep-alive
Upgrade-Insecure-Requests: 1
If-Modified-Since: Mon, 18 Jul 2016 02:36:04 GMT
If-None-Match: "c561c68d0ba92bbeb8b0fff2a9199f722e3a621a"
Cache-Control: max-age=0
```

[Conditional GET for RSS Hackers](https://fishbowl.pastiche.org/2002/10/21/http_conditional_get_for_rss_hackers)
>The mechanism for performing a conditional get has changed slightly between HTTP versions 1.0 and 1.1. Like many things that changed between 1.0 and 1.1, you really have to do both to make sure you're satisfying everybody.
>
>When you receive the RSS file from the webserver, check the response header for two fields: `Last-Modified` and `ETag`. You don't have to care what is in these headers, you just have to store them somewhere with the RSS file.
>
>Next time you request the RSS file, include two headers in your request.. Your `If-Modified-Since` header should contain the value you snagged from the `Last-Modified` header earlier. The `If-None-Match` header should contain the value you snagged from the `ETag` header.
>
>If the RSS file has changed since you last requested it, the server will send you back the new RSS file in the perfectly normal way. However, if the RSS file has not changed, the server will respond with a `304` response code (instead of the usual `200`), where `304` means ‘Not Modified’. In the case of a `304`, the response will have an empty body and the RSS file won't be sent back to you at all.
>
>There's a temptation for clients to put their own date in the `If-Modified-Since` header, instead of just copying the one the server sent. This is a bad thing, what you should be sending back is exactly the same date the server sent you when you received the file. There's two reasons for this. Firstly, your computer's clock is unlikely to be exactly synchronised with the webserver, so the server could still send you files by mistake. Secondly, if the server programmer has followed this guide (see below), it'll only work if you send back exactly what you received.

