# Table of content
```
1. Introduction
  1.1. Project overview
  1.2. Goals and objectives
  1.3. Resources
2. Test strategy
  2.1. Automation testing
  2.2. Manual testing
3. Iteration test plan
  3.1. Test cases
4. Test results
```

# 1. Introduction

## 1.1. Test overview

The execution of this plan should test an abandoned open source software, to see if it is stable and performant enough to be used by our client, _Software Development Company (SDC)_, for their intention of having a small web server for a wide range of Internet of Things applications.

## 1.2. Goals and objectives

Internet of Things applications are usually lower end hardware that does not need to handle extreme user load, but need to be reliable when accessed. As many IoT-application might not need to handle more than a maximum of a couple of hundred user simultaniously. So for this server application and test strategy, the Test Lead has set the minimum number of the server to handle to 200.

## 1.3. Resources

* Two persons, Tester #1 (Tester #1 will also act as Test Lead to make certain decisions) and Tester #2. One work week each, total of 80 hours.
* Ubuntu 16.04 operating system as testing platform.

# 2. Test plan

## 2.1. Test levels

The plan for this iteration is to perform manual tests to verify the current state of the web server application.

# 3. Test cases

## 3.1 The web server should be responsive under high load
Test-id: REQ1.1

### Description
The web server should be perform "desirably" when recieving HTTP requests from multiple user at once. The minimum number of request per second the application should be able to handle is 200. To ensure this, it is requested to test it under double that load.

Apache JMeter, or similar, should be used to during the performance and load tests.

### Pre-condition

_MyWebserver_ should be started with working contents.

### Test steps

1. Setup a JMeter 'test plan' for the webserver.
2. Set the 'Number of Threads' to 400 for a ramp-up period of 1 second.
3. Run the load tests.

### Expected Result
The webserver should _not_ fail (as in, not crash or report a failed status in JMeter), and the responses should not have an average latency higher than 30 milliseconds.

---

## 3.2 The web server must follow minimum requirements for HTTP 1.1
Test-id: REQ2.1

### Description
To get an accurate test of the HTTP protocol, Wireshark should be used to analyze the packets sent from the web server to verify that HTTP protocol version 1.1 or later is being used.

### Pre-condition

_MyWebserver_ should be started with working contents.

### Test steps

1. Setup Wireshark to listen to the trafic while accessing the web server.
2. Access the web server using any web browser.

### Expected Result

Wireshark analysis should show that HTTP 1.1 is used when requesting the webserver in the web browser, and respond with the same protocol.

---

## 3.3 The web server must work on Linux, Mac, Windows*.

Test-id: REQ3.1

### Description

To test the webserver on all required operating systems, some testing will have to be postponed to future iterations as the test team currently does not have access to all operating system in the requirements.

However, being a web server written in Java, the server _should_ work on all listed operating systems under the assumption that they have a proper installation of Java.

### Pre-condition

* Java version 1.7 or later installed on system for test.

### Test steps

1. x
2. x

### Expected Result
What it is...

---

## 3.4 The source code should be released under GPL-2.0.

Test-id: REQ4.1

### Description
The web server application should be released under GPL-2.0 for _SDC_. Control that the license of the abandonded server source code allows for this license.

### Test steps

1. Investigate abandonware source code.

### Expected Result

Should allow the license to be GPL-2.0

---

## 3.5 The access log should be viewable from a text editor.

Test-id: REQ5.1

### Description
decsription goes here...

### Pre-condition

### Test steps

1. x
2. x

### Expected Result
What it is...

---

## 3.5 Start server - Error on port taken

Test-id: UC1.1

### Description
decsription goes here...

### Pre-condition

### Test steps

1. x
2. x

### Expected Result
What it is...

---

## 3.6 Start server - Error on restricted resources

Test-id: UC1.2

### Description
decsription goes here...

### Pre-condition

### Test steps

1. x
2. x

### Expected Result
What it is...

---

## 3.6 Start server - Access log could not be written to

Test-id: UC1.3

### Description
decsription goes here...

### Pre-condition

### Test steps

1. x
2. x

### Expected Result
What it is...

---

# 4. Test results

## Requirement coverage matrix

| Req | Reqs tested | REQ1.1 | REQ2.1 | REQ3.1 | REQ5.1 | UC1.1 | UC1.2 | UC1.3 |
|-----|:-----------:|:------:|:------:|:------:|:------:|:-----:|:-----:|:-----:|
| **Test cases** | 2 | | | | | | | |
| REQ1.1 | | x | | | | | | |
| REQ2.1 | | | x | | | | | |
| REQ3.1 | | | | x | | | | |
| REQ4.1 | | | | | | x | | |

---

## 4.1 The web server should be responsive under high load

### Test-id: REQ1.1

The weberver holds up to the workload under the JMeter stresstest, and the average latency was reported to 18 millseconds with a deviation of up to 20 milliseconds at the most.

### Test result: Passed.

---

## 4.2 The web server must follow minimum requirements for HTTP 1.1

### Test-id: REQ2.1

Wireshark packet analysis shows that HTTP 1.1 is being used.

### Test result: Passed.

---

## 4.3 The web server must work on Linux, Mac, Windows*

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

### Test-id: REQ4.1

The abandonware is released under the MIT license, which allows for a GPL-2.0 sublicense. 

### Test result: Passed.

---

