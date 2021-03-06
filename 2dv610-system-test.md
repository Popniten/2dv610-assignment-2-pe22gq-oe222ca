# Table of content

- [1. Introduction](#1-introduction)
  - [1.1. Test overview](#11-test-overview)
  - [1.2. Goals and objectives](#12-goals-and-objectives)
  - [1.3. Resources](#13-resources)
- [2. Test plan](#2-test-plan)
  - [2.1. Test levels](#21-test-levels)
  - [2.2 What should not be tested](#22-what-should-not-be-tested)
- [3. Test cases](#3-test-cases)
  - [3.1 The web server should be responsive under high load](#31-the-web-server-should-be-responsive-under-high-load)
  - [3.2 The web server must follow minimum requirements for HTTP 1.1](#32-the-web-server-must-follow-minimum-requirements-for-http-11)
  - [3.3 The web server must work on Linux, Mac, Windows*.](#33-the-web-server-must-work-on-linux-mac-windows)
  - [3.4 The source code should be released under GPL-2.0.](#34-the-source-code-should-be-released-under-gpl-20)
  - [3.5 The access log should be viewable from a text editor.](#35-the-access-log-should-be-viewable-from-a-text-editor)
  - [3.6 Start server - System asks for socket port number and shared resource container](#36-start-server---system-asks-for-socket-port-number-and-shared-resource-container)
  - [3.7 Start server - System starts a web server on the given port and presents that the server was started and writes a note in the access log.](#37-start-server---system-starts-a-web-server-on-the-given-port-and-presents-that-the-server-was-started-and-writes-a-note-in-the-access-log)
  - [3.8 Start server - Error on port taken](#38-start-server---error-on-port-taken)
  - [3.9 Start server - Error on restricted resources](#39-start-server---error-on-restricted-resources)
  - [3.10 Start server - Access log could not be written to](#310-start-server---access-log-could-not-be-written-to)
  - [3.11 Stop server](#311-stop-server)
  - [3.12 Stop server](#312-stop-server)
  - [3.13 Request shared resource](#313-request-shared-resource)
  - [3.14 Request shared resource - 404 Not Found](#314-request-shared-resource---404-not-found)
  - [3.15 Request shared resource - 403 Forbidden](#315-request-shared-resource---403-forbidden)
  - [3.16 Request shared resource - 400 Bad Request](#316-request-shared-resource---400-bad-request)
- [4. Test results](#4-test-results)
  - [Requirement coverage matrix](#requirement-coverage-matrix)
  - [4.1 The web server should be responsive under high load](#41-the-web-server-should-be-responsive-under-high-load)
  - [4.2 The web server must follow minimum requirements for HTTP 1.1](#42-the-web-server-must-follow-minimum-requirements-for-http-11)
  - [4.3 The web server must work on Linux, Mac, Windows*](#43-the-web-server-must-work-on-linux-mac-windows)
  - [4.4 The source code should be released under GPL-2.0.](#44-the-source-code-should-be-released-under-gpl-20)
  - [4.5 The access log should be viewable from a text editor.](#45-the-access-log-should-be-viewable-from-a-text-editor)
  - [4.6 Start server - System asks for socket port number and shared resource container](#46-start-server---system-asks-for-socket-port-number-and-shared-resource-container)
  - [4.7 Start server - System starts a web server...](#47-start-server---system-starts-a-web-server)
  - [4.8 Start server - Error on port taken](#48-start-server---error-on-port-taken)
  - [4.9 Start server - Error on restricted resources](#49-start-server---error-on-restricted-resources)
  - [4.10 Start server - The access log could not be written to](#410-start-server---the-access-log-could-not-be-written-to)
  - [4.11 Stop server](#411-stop-server)
  - [4.12 Stop server](#412-stop-server)
  - [4.13 Request shared resource](#413-request-shared-resource)
  - [4.14 Request shared resource - 404 Not Found](#414-request-shared-resource---404-not-found)
  - [4.15 Request shared resource - 403 Forbidden](#415-request-shared-resource---403-forbidden)
  - [4.16 Request shared resource - 400 Bad Request](#416-request-shared-resource---400-bad-request)

# 1. Introduction

## 1.1. Test overview

The execution of this plan should test an abandoned open source software, to see if it is stable and performant enough to be used by our client, _Software Development Company (SDC)_, for their intention of having a small web server for a wide range of Internet of Things applications and hardware.

## 1.2. Goals and objectives

Internet of Things applications are usually lower end hardware that does not need to handle extreme user load, but need to be reliable when accessed. As many IoT-application might not need to handle more than a maximum of a couple of hundred user simultaneously. So for this server application and test strategy, the Test Lead has set the minimum number of the server to handle to 200.

The goal of the test plan is to see if the abandoned server software is suitable for _SDC_ to use for their IoT applications, and outline what bugs exists in the web server. This is needed to plan for further development of the server application, if it is deemed good enough by the stakeholders.

## 1.3. Resources

* Two persons, Tester #1 (Tester #1 will also act as Test Lead to make certain decisions) and Tester #2. One work week each, total of 80 hours.
* Ubuntu 16.04 operating system as testing platform.
* Postman Chrome plugin for API testing.
* Wireshark
* Apache JMeter

# 2. Test plan

## 2.1. Test levels

The plan for this iteration is to perform manual tests to verify the current state of the web server application.

All the tests will be performed by Tester #1 and Tester #2.

## 2.2 What should not be tested

In use case 3 part 2d, it is stated that an 500 internal error should be presented. This is very difficult to produce using the web browser and therefor the Test Lead has decided that there is no need to test it.

# 3. Test cases

The test case IDs are a direct reference to the requirements document, and the requirements and use cases in there.

## 3.1 The web server should be responsive under high load
Test-id: REQ1.1

### Description
The web server should be perform "desirably" when receiving HTTP requests from multiple user at once. The minimum number of request per second the application should be able to handle is 200. To ensure this, it is requested to test it under double that load.

Apache JMeter, or similar, should be used to during the performance and load tests.

### Precondition

_MyWebserver_ should be started with working contents.

### Test steps

1. Setup a JMeter 'test plan' for the web server.
2. Set the 'Number of Threads' to 400 for a ramp-up period of 1 second.
3. Run the load tests.

### Expected Result
The web server should _not_ fail (as in, not crash or report a failed status in JMeter), and the responses should not have an average latency higher than 30 milliseconds.

---

## 3.2 The web server must follow minimum requirements for HTTP 1.1
Test-id: REQ2.1

### Description
To get an accurate test of the HTTP protocol, Wireshark should be used to analyze the packets sent from the web server to verify that HTTP protocol version 1.1 or later is being used.

### Precondition

_MyWebserver_ should be started with working contents.

### Test steps

1. Setup Wireshark to listen to the traffic while accessing the web server.
2. Access the web server using any web browser.

### Expected Result

Wireshark analysis should show that HTTP 1.1 is used when requesting the web server in the web browser, and respond with the same protocol.

---

## 3.3 The web server must work on Linux, Mac, Windows*.

Test-id: REQ3.1

### Description

To test the web server on all required operating systems, some testing will have to be postponed to future iterations as the test team currently does not have access to all operating system in the requirements.

However, being a web server written in Java, the server _should_ work on all listed operating systems under the assumption that they have a proper installation of Java.

### Precondition

* Java version 1.7 or later installed on system for test.

### Test steps

1. Start the web server with the command `java -jar server.jar PORT RESOURCE`

### Expected Result
The web server should launch and serve contents on the specific operating system.

---

## 3.4 The source code should be released under GPL-2.0.

Test-id: REQ4.1

### Description
The web server application should be released under GPL-2.0 for _SDC_. Control that the license of the abandoned server source code allows for this license.

### Test steps

1. Investigate abandonware source code.

### Expected Result

Should allow the license to be GPL-2.0

---

## 3.5 The access log should be viewable from a text editor.

Test-id: REQ5.1

### Description
The system should have a access log that you can access and read from a text editor.

### Precondition
Started server with working content
Some test-access visits

### Test steps

1. Open access log
2. Read access log

### Expected Result
The access log should be readable.

---

## 3.6 Start server - System asks for socket port number and shared resource container

Test-id: UC1.2

### Description

When starting a server using the command `java -jar server.jar`, the system should ask for a port to use as well as a folder with website resources.

### Test steps

1. Start the server.
2. Enter a port number.
3. Enter a resource location.

### Expected Result

The server should start with the given port and resource folder.

---

## 3.7 Start server - System starts a web server on the given port and presents that the server was started and writes a note in the access log.

Test-id: UC1.4

### Description

Start the server with a given port and resource.

### Test steps

1. Launch server with a given port and resource
2. Check output message.
3. Check access log for note.

### Expected Result

The server should print out a message that it has started and add that to the access log.

---

## 3.8 Start server - Error on port taken

Test-id: UC1.4a

### Description
If we try to start the server on a port that is taken we need the system to show this in an output.

### Precondition

### Test steps

1. Launch server with taken port
2. Check output

### Expected Result
The system output should be “Socket XX was taken” (XX is the socket number, Example “80”)

---

## 3.9 Start server - Error on restricted resources

Test-id: UC1.4b

### Description
When trying to start a web server using a resource folder with insufficient rights, the server should present an error message that it cannot access the resources.

### Precondition

Start a server using a folder with no read or write permissions for the user starting the server.

### Test steps

1. Start the server using faulty folder permissions.

### Expected Result

Server should present an error message saying "No access to folder _/folderName_".

---

## 3.10 Start server - Access log could not be written to

Test-id: UC1.4c

### Description

If the system does not have write permissions on the `log.txt` there should be an error message printed.

### Precondition

Server started with no read/write permissions on the resource folder.

### Test steps

1. Start server.
2. Check for error message about accessing the log file.

### Expected Result

System presents an error message. “Cannot write to server log file log.txt”

---

## 3.11 Stop server

Test-id: UC2.1

### Description

When the administrator stops the web server, the system should inform the administrator that the server has successfully stopped.

### Precondition

A web server should be started.

### Test steps

1. In the terminal, write `stop` to stop the server.
2. Check the output.

### Expected Result

The system should print a stop message.

---

## 3.12 Stop server

Test-id: UC2.2

### Description

When the server is stopped, it should be noted in the access log.

### Precondition

The test case UC2.1 should have been performed.

### Test steps

1. Perform the test UC2.1
2. Check the access log for a note that the server has stopped.

### Expected Result

Access log should contain a stop message.

---

## 3.13 Request shared resource

Test-id: UC3.2

### Description

The server should deliver the shared resource to the web browser when a user accesses the website.

### Precondition

A web server should be started.

### Test steps

1. Access the website in a web browser.
2. Check that content is served.

### Expected Result

Content should be visible in the browser, and a message should be written to the access log.

---

## 3.14 Request shared resource - 404 Not Found

Test-id: UC3.2a

### Description

When trying to access a resource that does not exist, an error message should be presented to the browser user.

### Precondition

A web server should be started.

### Test steps

1. Access a non-existing resource in a web browser.
2. Check that error message is served.

### Expected Result

A `404 Not Found` should be presented in the web browser.

---

## 3.15 Request shared resource - 403 Forbidden

Test-id: UC3.2b

### Description

When trying to access a resource that the server does not have read permissions on, the user should get a message that access is forbidden.

### Precondition

A web server should be started. A resource with restricted permissions should be present.

### Test steps

1. Access restricted resource.
2. Web server should present the user with an error message.

### Expected Result

A `403 Forbidden` should be presented in the web browser.

---

## 3.16 Request shared resource - 400 Bad Request

Test-id: UC3.2c

### Description

If trying to access the server with an invalid request, the server should respond with an error message.

### Precondition

A web server should be started.

### Test steps

1. Use Postman to send a PURGE request to the web server.
2. Observe the response from the web server.

### Expected Result

A `400 Bad Request` response status should be returned.

---

# 4. Test results

## Requirement coverage matrix

|Reqs|Reqs Tested|REQ1.1|REQ2.1|REQ3.1|REQ4.1|REQ5.1|UC1.2|UC1.4|UC1.4a|UC1.4b|UC1.4c |UC2.1|UC2.2|UC3.2|UC3.2a|UC3.2b|UC3.2c|
|---|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|**Test cases**| 16 |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|REQ1.1|   | ✓ |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|REQ2.1|   |   | ✓ |   |   |   |   |   |   |   |   |   |   |   |   |   |   |
|REQ3.1|   |   |   | × |   |   |   |   |   |   |   |   |   |   |   |   |   |
|REQ4.1|   |   |   |   | ✓ |   |   |   |   |   |   |   |   |   |   |   |   |
|REQ5.1|   |   |   |   |   | × |   |   |   |   |   |   |   |   |   |   |   |
|UC1.2|    |   |   |   |   |   | × |   |   |   |   |   |   |   |   |   |   |
|UC1.4|    |   |   |   |   |   |   | × |   |   |   |   |   |   |   |   |   |
|UC1.4a|   |   |   |   |   |   |   |   | × |   |   |   |   |   |   |   |   |
|UC1.4b|   |   |   |   |   |   |   |   |   | × |   |   |   |   |   |   |   |
|UC1.4c|   |   |   |   |   |   |   |   |   |   | × |   |   |   |   |   |   |
|UC2.1|    |   |   |   |   |   |   |   |   |   |   | ✓ |   |   |   |   |   |
|UC2.2|    |   |   |   |   |   |   |   |   |   |   |   | × |   |   |   |   |
|UC3.2|    |   |   |   |   |   |   |   |   |   |   |   |   | × |   |   |   |
|UC3.2a|   |   |   |   |   |   |   |   |   |   |   |   |   |   | ✓ |   |   |
|UC3.2b|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   | × |   |
|UC3.2c|   |   |   |   |   |   |   |   |   |   |   |   |   |   |   |   | × |

✓ = Passed test.
× = Failed test.

Total number of tests: _16_. Passed: _5_. Failed: _11_.

---

## 4.1 The web server should be responsive under high load

Test performed by: Tester #1

### Test-id: REQ1.1

The web server holds up to the workload under the JMeter stress test, and the average latency was reported to 18 milliseconds with a deviation of up to 20 milliseconds at the most.

### Test result: Passed.

---

## 4.2 The web server must follow minimum requirements for HTTP 1.1

Test performed by: Tester #1

### Test-id: REQ2.1

Wireshark packet analysis shows that HTTP 1.1 is being used.

### Test result: Passed.

---

## 4.3 The web server must work on Linux, Mac, Windows*

Test performed by: Tester #2

### Test-id: REQ3.1

As of this iteration, the test team did not have access to all required operating systems, therefor further testing is required in coming iterations.

* Ubuntu 16.04: Passed
* Linux Mint: N/A
* MacOS: N/A
* Windows 7: N/A
* Windows 10: N/A
* ...

### Test result: Pending...

---

## 4.4 The source code should be released under GPL-2.0.

Test performed by: Tester #1

### Test-id: REQ4.1

The abandonware is released under the MIT license, which allows for a GPL-2.0 sub-license.

### Test result: Passed.

---

## 4.5 The access log should be viewable from a text editor.

Test performed by: Tester #2

### Test-id: REQ5.1

There is no access log in the system.

### Test result: Failed.

---

## 4.6 Start server - System asks for socket port number and shared resource container

Test performed by: Tester #2

### Test-id: UC1.2

The server does not start without giving the port and resource as arguments to the start command. The system throws an exception without them.

### Test result: Failed.

---

## 4.7 Start server - System starts a web server...

Test performed by: Tester #1

### Test-id: UC1.4

The system prints out:

```
HTTP Server object constructed
HTTP Server started
Accept
```

But there is no output to the access log (which does not exist).

### Test result: Failed.

---

## 4.8 Start server - Error on port taken

Test performed by: Tester #2

### Test-id: UC1.4a

There is output indicating that the port is taken, however, it only shows "Port is taken" - not the port number being used.

### Test result: Failed.

---

## 4.9 Start server - Error on restricted resources

Test performed by: Tester #1

### Test-id: UC1.4b

The server starts without any error messages displayed, but when accessing the website in the browser, the user gets a 404 message there instead.

### Test result: Failed.

---

## 4.10 Start server - The access log could not be written to

Test performed by: Tester #1

### Test-id: UC1.4c

Could not perform this test accurately as the system has not yet implemented the access log.

### Test result: Failed.

---

## 4.11 Stop server

Test performed by: Tester #2

### Test-id: UC2.1

System prints out:

```
HTTP Server Accept thread stopped
HTTP Server stopped
```

### Test result: Passed.

---

## 4.12 Stop server

Test performed by: Tester #1

### Test-id: UC2.2

Access log could not be accessed.

### Test result: Failed.

---

## 4.13 Request shared resource

Test performed by: Tester #2

### Test-id: UC3.2

Content is visible in the browser, but the system failed to write to the log file.

### Test result: Failed.

---

## 4.14 Request shared resource - 404 Not Found

Test performed by: Tester #1

### Test-id: UC3.2a

A 404-message is correctly being displayed.

### Test result: Passed.

---

## 4.15 Request shared resource - 403 Forbidden

Test performed by: Tester #2

### Test-id: UC3.2b

A faulty message was presented, instead of a 403 the result was that the server `unexpectedly closed the connection`.

### Test result: Failed.

---

## 4.16 Request shared resource - 400 Bad Request

Test performed by: Tester #1

### Test-id: UC3.2c

A `400 Bad Request` was returned from the server using Postman.

### Test result: Passed.

---
