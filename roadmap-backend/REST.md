# *

- [http method](#http-method)
- [http response](#http-response)
  - [status code](#status-code)
- [url](#url)
  - [versioning](#versioning)

[exposing database ids (about security)](https://stackoverflow.com/questions/396164/exposing-database-ids-security-risk) (exposes data size, see also [this](https://stackoverflow.com/questions/56576985/is-it-a-bad-practice-to-expose-the-database-id-to-the-client-in-your-rest-api)

[custom header v.s. query parameter](https://stackoverflow.com/questions/9169081/rest-apis-custom-http-headers-vs-url-parameters)

[The only rule you should obey is that a custom header should begin by `X-`](https://stackoverflow.com/a/37168084)

max payload size? [no limit in the standard (RFC 2616), differs per implementation](https://stackoverflow.com/questions/1495541/rest-payload-max-size)

## http method

知乎 - [我所在的公司规定所有接口都用 post 请求](https://www.zhihu.com/question/336797348)

耗子 coolshell - [rest api post 一把梭](https://coolshell.cn/articles/22173.html)

[POST with url query params, good idea or not?](https://stackoverflow.com/questions/611906/http-post-with-url-query-parameters-good-idea-or-not)

DELETE multiple records?

1. [Nicholas suggests not to do this](https://stackoverflow.com/a/21863914)
2. [Decent suggests two-step-approaches](https://stackoverflow.com/a/2445682)
3. [DELETE can potentially have the body ignored by the infra](http://stackoverflow.com/questions/299628/is-an-entity-body-allowed-for-an-http-delete-request)

## http response

[should no results be an error?](https://softwareengineering.stackexchange.com/questions/358243/should-no-results-be-an-error-in-a-restful-response)

[any standard for json api response format?](https://stackoverflow.com/questions/12806386/is-there-any-standard-for-json-api-response-format)

### status code

[proper response code for a valid request but an empty data?](https://stackoverflow.com/questions/11746894/what-is-the-proper-rest-response-code-for-a-valid-request-but-an-empty-data)

[appropriate http status code --> logging in](https://stackoverflow.com/questions/32752578/whats-the-appropriate-http-status-code-to-return-if-a-user-tries-logging-in-wit)

## URL

[use hyphen, underscore or camelcase in url?](https://stackoverflow.com/questions/10302179/hyphen-underscore-or-camelcase-as-word-delimiter-in-uris)

[endpoint can be different for different HTTP methods](https://stackoverflow.com/a/47573997/11844003)

Endpoint values which contain a leading `/` are absolute. Absolute values retain only the `host` from `baseUrl` and ignore any specified path components.

### versioning

[best practice, api versioning](https://stackoverflow.com/questions/389169/best-practices-for-api-versioning)

## helping links

- [http cats](https://http.cat/)
- [Google JSON Guid](https://google.github.io/styleguide/jsoncstyleguide.xml)
