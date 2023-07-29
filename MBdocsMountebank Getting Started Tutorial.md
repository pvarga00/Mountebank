
# Greetings!

If you are reading this then you must be interested in setting up service virtualization with Mountebank.

Before we get started, please give the front page of [http://www.mbtest.org/](http://www.mbtest.org/) a quick read.

Specifically pay attention to this:

<ac:image ac:alt="mountebank"><ri:url ri:value="http://www.mbtest.org/images/overview.gif"></ri:url></ac:image>

This image sums up how Mountebank works.

## **<u>Installing Mountebank</u>**

Check out our "<ac:link><ri:page ri:space-key="SV" ri:content-title="Mountebank: Installation"></ri:page><ac:plain-text-link-body><![CDATA[How to Install Mountebank]]></ac:plain-text-link-body></ac:link>" guides (either locally or AWS hosted)

## **<u>Stuff to keep in mind before we get started:</u>**

Terminal == Command Prompt. We will be using one term in this tutorial for simplicity.

MB == Mountebank

Service Virtualization == HTTP/API Mocking

## <u>Lexicon (Definitions)</u>

imposter == A server representing a test double. An imposter is identified by a port and a protocol. mountebank is non-modal and can create as many imposters as your test requires.

stub == A set of configuration used to generate a response for an imposter. An imposter can have 0 or more stubs, each of which are associated with different predicates.

predicate == A condition that determines whether a given stub is responsible for responding. Each stub can have 0 or more predicates.

response == The configuration that generates the response for a stub. Each stub can have 0 or more responses.

response type == Defines the specific type of configuration used to generate a response. The simplest type is called is, and allows you to define the imposter's response directly. mountebank also supports a proxy response type, which allows record-replay behavior, and an inject response type, which allows you to script mountebank responses. Each response has exactly one response type.

stub behavior == Adds additional post-processing to a response, for example by adding latency to the response or augmenting the response with more information. A response can have zero or more behaviors, but only one of each type of behavior.



## **<u>Using Mountebank: Your First Lesson!</u>**

*(You can find the original documentation here: [http://www.mbtest.org/docs/gettingStarted](http://www.mbtest.org/docs/gettingStarted) - below, we've "Quicken-ized" the original content)*



**Running Mountebank:**

From a terminal window or command prompt (Powershell), launch Mountebank:


> ```
> mb
> ```


By default, mountebank listens on port 2525, but that's not the port that your imposters (test doubles) will listen on. To show a couple different kinds of imposters, let's create both an http imposter and a tcp one.

We'll use the `curl` command line tool to call mountebank's [api](http://www.mbtest.org/docs/api/overview). The following command creates the http imposter, listening on port 4545, by `POST`ing to [http://localhost:2525/imposters](http://localhost:2525/imposters) with the given body.

The `predicates` are optional - if you don't include any, the stub always matches, and the response is always sent.



The [contracts page](http://www.mbtest.org/docs/api/contracts) provides an easy to use exploration of the JSON structure.


> ```
> curl -i -X POST -H 'Content-Type: application/json' http://localhost:2525/imposters --data '{
>   "port": 4545,
>   "protocol": "http",
>   "stubs": [{
>     "responses": [
>       { "is": { "statusCode": 400 }}
>     ],
>     "predicates": [{
>       "and": [
>         {
>           "equals": {
>             "path": "/test",
>             "method": "POST",
>             "headers": { "Content-Type": "application/json" }
>           }
>         },
>         {
>           "not": {
>             "contains": { "body": "requiredField" },
>             "caseSensitive": true
>           }
>         }
>       ]
>     }]
>   }]
> }'
> ```


Let's test it out:


> ```
> curl -i -X POST -H 'Content-Type: application/json' http://localhost:4545/test --data '{"optionalField": true}'
> ```


```

```


> ```
> HTTP/1.1 400 Bad Request
> Connection: close
> Date: Sat, 04 Jan 2014 02:48:16 GMT
> Transfer-Encoding: chunked
> ```




Had we not tailored the request to match the predicates, we would have instead received the default response. For instance, let's send a request that leaves off the Content-Type:


> ```
> curl -i -X POST http://localhost:4545/test --data '{"optionalField": true}'
> ```


```

```


> ```
> HTTP/1.1 200 OK
> Connection: close
> Date: Sat, 04 Jan 2014 02:48:16 GMT
> Transfer-Encoding: chunked
> ```




Mountebank can stub binary tcp equally well, which is convenient when your application integrates with a downstream system using one of the myriad binary RPC protocols. Those protocols tend to rely on language-specific serialization to return an object graph. Your test can use the same serialization code to create a binary stream of the object you want the imposter to return during an RPC call, and encode it as a base64 string. That string is what you send to the imposter. In the example below, we're telling the imposter to respond with a base64-encoded string of "hello, world!" when a tcp request containing the string "sayHello" is sent to port 5555, which could correspond to the method name serialized in the RPC call:


> ```
> curl -i -X POST -H 'Content-Type: application/json' http://localhost:2525/imposters --data '{
>   "port": 5555,
>   "protocol": "tcp",
>   "mode": "binary",
>   "stubs": [{
>     "responses": [
>       { "is": { "data": "aGVsbG8sIHdvcmxkIQ==" }}
>     ],
>     "predicates": [{ "contains": { "data": "c2F5SGVsbG8=" } }]
>   }]
> }'
> ```


We'll use `nc` (netcat) to make the tcp request, which is like `telnet` but easier to script.


> ```
> echo "Calling sayHello over binary protocol" | nc localhost 5555
> ```


```

```


> ```
> hello, world!
> ```




Finally, we can shut down both imposters by issuing an HTTP `DELETE` to both imposters, which are identified by the port number on the URL:


> ```
> curl -X DELETE http://localhost:2525/imposters/4545
> curl -X DELETE http://localhost:2525/imposters/5555
> ```




Explore more in the links on the left. And please don't hesitate to [ask](mailto:ItTeamQAPOW@quickenloans.com) for help! (Psst, you can totally bug these folks, they'll be happy to help! : [ItTeamQAPOW@quickenloans.com](mailto:ItTeamQAPOW@quickenloans.com))



You can also explore the [Mountebank Google Group here](https://groups.google.com/forum/#!forum/mountebank-discuss)

**<u><br></u>**
