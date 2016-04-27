# my-api

**Warning: This code works for Mule ESB 3.7.2 EE so you need Enterprise level subscription to dowload the MUnit dependencies**

Mule API to show the configuration is needed to implement MUnit for testing and the project layout it's being used
for my Mule Projects.

MUnit emerged as the standard testing tool for Mule applications with the idea of writing Mule flows
to test themselves which sounds great since Mule provides a full set of tools to send, receive and process messages.

Based on https://docs.mulesoft.com/munit/v/1.1.1/example-testing-apikit I started writing Unit tests for one of my
APIs but found domain-based applications are not supported. The workaround to make it work from Studio is a matter to
add a copy of the HTTP connector is used by the API either in the same test file or a separated one.
I added `src/test/munit/munit-support.xml` and worked fine, however, also tried to make it work from the command line
since the application should be built and deployed by a Jenkins server.
In order to do that and not to modify the original code I ended up adding additional dependencies in `pom.xml` and also
added a copy of `mule-deploy.properties` underneath `src/test/munit` which includes the additional xml was added as follows:

`config.resources=my-api.xml,global-config.xml,munit-support.xml`

This is done to avoid including `munit-support.xml` in the final build.

The bad thing about this approach is Studio shows a warning with the duplicated `mule-deploy.properties` (I hate warnings)

MUnit is still evolving and adding new features with every release like Coverage. The product looks promising and
implementing Unit tests for Mule applications never been easier.
