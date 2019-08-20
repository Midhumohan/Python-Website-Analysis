# Request Module

Requests is a Python module that you can use to send all kinds of HTTP requests. It is an easy-to-use library with a lot of features ranging from passing parameters in URLs to sending custom headers and SSL Verification.

```bash

import requests
response = requests.get(url,timeout=2)
   

`````
## Python script to fetch the staus code of the websites and the time taken to execute the code using Request module. 

```bash

import requests
import time

start = time.time()

urls = [
  'https://www.redhat.com',
  'https://ubuntu.com',
  'https://www.kali.org',
  'https://www.centos.org',
  'https://www.debian.org',
  'https://www.linuxmint.com',
  'https://www.tecmint.com',
  'https://www.udemy.com',
  'https://tutorials.ubuntu.com'
]


statusDict = {}

for url in urls:
  
  try:
    
    response = requests.get(url,timeout=2)
    status = response.status_code
    statusDict[url] = status
    
  except:
    
    pass

for url in statusDict:
  status = statusDict[url]
  print('{:4} {}'.format(status,url))
  
end = time.time()

total_time = end - start

print('Total Time Taken : {}'.format(total_time))

`````


## Result

```bash
200 https://www.redhat.com
 200 https://ubuntu.com
 403 https://www.kali.org
 200 https://www.centos.org
 200 https://www.debian.org
 200 https://www.linuxmint.com
 200 https://www.tecmint.com
 403 https://www.udemy.com
 200 https://tutorials.ubuntu.com
Total Time Taken : 13.57437252998352

````

# Threding in Python

Threading in python is used to run multiple threads (tasks, function calls) at the same time.

To create a new thread, we create an object of Thread class. It takes following arguments: target: the function to be executed by thread.

```bash

import threading
t = threading.Thread(target=getStatus,args=(url,))
t.start()

````


## python script to fetch the staus code of the websites and the time taken to execute the code using threading. 

```bash

import requests
import time
import threading

start = time.time()

urls = [
  'https://www.redhat.com',
  'https://ubuntu.com',
  'https://www.kali.org',
  'https://www.centos.org',
  'https://www.debian.org',
  'https://www.linuxmint.com',
  'https://www.tecmint.com',
  'https://www.udemy.com',
  'https://tutorials.ubuntu.com'
]
statusDict = {}

threadList = []

def getStatus(url):
    
    try:
    
      response = requests.get(url,timeout=2)
      status = response.status_code
      statusDict[url] = status
    
    except:
    
      statusDict[url] = 'Error'
  
  
for url in urls:

  t = threading.Thread(target=getStatus,args=(url,))
  t.start()
  threadList.append(t)
  
  
for thread in threadList:
  thread.join()
  
for url in statusDict:
  status = statusDict[url]
  print('{:4} {}'.format(status,url))
  
end = time.time()

total_time = end - start

print('Total Time Taken : {}'.format(total_time))

````

## Result

```bash

403 https://www.kali.org
 403 https://www.udemy.com
 200 https://www.linuxmint.com
 200 https://www.tecmint.com
 200 https://www.centos.org
 200 https://www.debian.org
 200 https://ubuntu.com
 200 https://tutorials.ubuntu.com
 200 https://www.redhat.com
Total Time Taken : 2.601806163787842

````

