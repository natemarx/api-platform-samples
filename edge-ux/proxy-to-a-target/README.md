# Proxy to a target service

Think "Hello World". This very simple API proxy calls a backend target. This is the core of what proxies do.

### What's interesting about this sample

* To define a backend target, this sample includes a TargetEndpoint in a file called `apiproxy/targets/default.xml`. In that file, this XML block specifies the target of the proxy, a web service called `mocktarget.apigee.net`:

   ```xml
   <TargetEndpoint name="default">
      <HTTPTargetConnection>
        <!-- This is where we define the target. For this sample we just use a simple URL. -->
        <URL>http://mocktarget.apigee.net</URL>
      </HTTPTargetConnection>
   </TargetEndpoint>```

* To connect the target to this proxy, the proxy refers to the target in its `<RouteRule>` element. You'll find that code in the `apiproxy/proxies/default.xml` file. The `<TargetEndpoint>` element's value is "default" -- the `name` attribute value of the TargetEndpoint.

   ```xml
   <RouteRule name="default">
        <!-- This connects our proxy to the target defined in apiproxy/targets/default.xml -->
        <TargetEndpoint>default</TargetEndpoint>
   </RouteRule>
   ```
   
> **What's a revision?** You might notice that when you deployed `proxy-to-a-target` you created a new revision of the proxy with the name `learn-edge`. The deploy script just creates a new revision each time it deploys. If you want to go back to a previous revision, you can go to the Edge UI and select it from the **Revision** menu. Or, you can just redeploy whichever proxy you want to use from the command-line -- and it will become the current revision.

### Extra reading: important terms and concepts

* [**What's an API proxy?**](http://docs.apigee.com/api-services/content/understanding-apis-and-api-proxies#whatisanapiproxy) -- An API proxy is a way to expose APIs for loose coupling, security, and performance.
* **Target service** -- A backend service that the proxy calls on behalf of the requesting app. Here, we're going to return data from a service called `mocktarget.apigee.net`. 
* [**TargetEndpoint**](https://docs.apigee.com/api-services/reference/api-proxy-configuration-reference#targetendpoint) -- The name of a target definition in the apiproxy/targets directory. 
* [**RouteRule**](http://docs.apigee.com/api-services/content/understanding-routes#determiningtheurlofthetargetendpoint) -- Specifies which target endpoint definition file to call. Route rules can have logic to route calls conditionally to different targets. 
* [**HTTPTargetConnection**](https://docs.apigee.com/api-services/reference/api-proxy-configuration-reference#targetendpoint-targetendpointconfigurationelements) -- Defines the target to which to send the request. Usually a URL. 

### Other things to try

* In a browser, hit http://mocktarget.apigee.net/help to see what else the service can do. 
* Try changing the proxy to call another REST-based backend service of your choosing. Test the change (redeploy and invoke). Hint: Edit `apiproxy/targets/default.xml`.

### Ask the community

[![alt text](../../images/apigee-community.png "Apigee Community is a great place to ask questions and find answers about developing API proxies. ")](https://community.apigee.com?via=github)

---

Copyright © 2016 Apigee Corporation

Licensed under the Apache License, Version 2.0 (the "License"); you may not use
this file except in compliance with the License. You may obtain a copy
of the License at

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.