## 3.4 The access log should be viewable from a text editor.

Test-id: REQ5.1

### Description
The system should have a access log that you can access and read from a text editor.

### Pre-condition
Started server with wortking content
Some test-access visits

### Test steps

1. Open access log
2. Read access log

### Expected Result
The access log should be readable.

---

## 3.5 Start server - Error on port taken

Test-id: UC1.1

### Description
If we try to start the server on a port that is taken we need the system to show this in an output. 

### Pre-condition

### Test steps

1. Launch server with taken port
2. Check output

### Expected Result
The system output should be “Socket XX was taken” (XX is the socket number, Example “80”)

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

# Test results


---

## x.x 

### Test-id: REQ5.1

There is no access log in the system.

### Test result: Failed.

---

## x.x 

### Test-id: UC1.1

There is output indicating that the port is taken, however, it only shows "Port is taken" - not the port number being used.

### Test result: Failed.

