
**Question:**How does Service Virtualization relate to SOA?

**Answer:**

"Service Virtualization" (SV) is a way to emulate (fake) the behavior of specific components in most API-driven applications, cloud-based applications, and service-oriented architectures (SOA), by providing "mock" or canned responses to API requests.

SV is used to provide software development and QA/testing teams access to dependent system components that are needed to exercise an application under test (AUT), but are unavailable or difficult-to-access for development and testing purposes (think: click-charged API calls, or PROD only dependency systems).

With the behavior of the dependent components "virtualized," testing and development can proceed without accessing the actual "live" components/systems - by leveraging the mocked (imposter) responses instead. This is especially useful in testing certain scenarios about how a system will react (fail gracefully) - when a dependent system is no longer accessible or providing slow response times (which can be mocked) – allowing the "real/actual" system to behave normally.



**Question:**Elaborate what it means by "hard to reach" spaces?

**Answer:** Like when washing our backs? Just kidding. "Hard-to-reach spaces" refers to systems that are not easily testable under "normal circumstances".

Such constraints occur in complex, inter-dependent environments when a component connected to the application under test is:

- Not yet completed/available (Gump: The dependent system is still evolving / under development / not deployed)
- Controlled by a third-party or partner
- Available for testing only in limited capacity, at inconvenient times, or with diminished available test cases
- Difficult to provision or configure within test environment(s)
- Needed for simultaneous access by different teams, with varied test data setup and other requirements (Think: slow response times, always available responses, etc.)
- Restricted or costly to use for load and performance testing (Think: "Click charging")




**Question:**What is the difference between running an imposter on this platform, versus what are are doing now?

**Answer:** Historically, we've relied on ALL of our systems being ready, deployed, and actively available during our testing. This means that we needed to deploy all systems, together, interdependently. With Mountebank (the tooling we've selected in order to accomplish SV), we can decouple the need for downstream systems/data/scenarios being available, in order to understand how our systems behave under testing.

For example: Let's say we are supporting Yelp - with the dependency of Google Maps of finding restaurant locations. If we experienced an outage/slowdown with Google Maps, would our application (Yelp), be able to still process requests for information, or maybe failover to another geo-location provider (Waze, OsmAnd, etc.), or would Yelp fail completely? Our clients would expect that OUR application, Yelp -- just plain works... regardless of whatever Google Maps does (to our application).

Mountebank allows us to answer these questions, without actually BEING in the "bad situation" first - but testing for it nonetheless!



**Question:**What are the benefits to running a test through Mountebank instead of a real dependency?

**Answer:** (see above? This feels like we already answered it)



**Question:**Explain this GIF that is posted to the site. What does this tell us?

<ac:image ac:height="235"><ri:attachment ri:filename="image2019-5-15_12-47-15.png"></ri:attachment></ac:image>

MAGIC!!!!!

<ac:image ac:alt="Image result for magic" ac:width="125"><ri:url ri:value="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS-6_hgFEML-w_RHkarGhGOCBtZjuSCNB1yakOHrOnkRCDV_FNt"></ri:url></ac:image>

Mountebank provides the ability for API tests that typically make requests to an application, to instead call an "imposter" (gump: "A test double" - which is like a stunt double in acting). An imposter can be thought of as a server representing a test double. An *imposter* is identified by a port and a protocol. Mountebank is non-modal and can create as many *imposters* as your test requires. An imposter is a pre-configured response to any request, with additional, optional post-processing information (ex: we can add additional latency to the response)

In the image, we see a "test" that makes API requests to an "app". The "app" would then send an API response back to the test, which can be verified as a correct response, or not. Things that can be tested in a response are: return codes (status of the request/response), headers, type, body, response times, etc.

Mountebank can then be used to intercept or proxy the requests a test makes to an "app" - and instead of expecting the "app" to provide a response, Mountebank provides the response it has for the "imposter" instead. This is where the "magic' happens, as we can provide many types of "mocked responses" for an "app".



**Question:** Which OKR does this speak to, and how will it help us achieve the OKR?

**Answer:** Possibly the best OKR this initiative falls under is: "Enterprise Services works collaboratively to deliver packaged solutions that enable our clients move faster and with certainty." - SV offers our applications the ability to test with certainty, faster, and with less dependencies!


