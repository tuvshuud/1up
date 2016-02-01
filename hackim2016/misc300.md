### misc 300 - Know India

It's question-and-answer programming challenge about India.

We wrote simple python script to answer all the questions.
```python
# -*- coding: utf8 -*-
import socket
s = socket.socket()
host = '52.91.163.151'
port = 10101

s.connect((host, port))

answers = ['tamil', 'english', 'kumbh mela', 'electronic city of india', 'wine capital of india', 'blue city', 'chenab', 'diamond city of india', 'dehradun', 'rock fort city', 'hindi', 'republic of india', 'abode of the god', 'english', 'port blair', 'second bardoli of india', 'chandigarh', 'agartala', 'city of paddy fields', 'gateway of north east india', 'tea city of india', 'boston of india', 'hindi', 'land of black diamond', 'hindi', 'english', 'gateway of south india', 'gangtok', 'prince of arabian sea', 'tamil', 'pink city', 'hindi', 'abode of the god', 'evergreen city of india', 'meiteilon', 'hindi', 'konkani', 'rome of the east', 'punjabi', 'telugu', 'gandhinagar', 'shillong', '1033', 'ganga', 'dal lake']

dictionary = {}
answer_from_dict = False
idx = 0
print s.recv(1024)
while True:
	answer_from_dict = False
	print 'Question #%d' % idx
	question = s.recv(1024)
	print question
	if dictionary.has_key(question):
		answer = dictionary[question]
		answer_from_dict = True
	else:
		answer = answers[idx]
	print 'Answer: %s' % answer
	s.send(answer.lower().encode('utf-8'))
	dictionary[question] = answer
	print s.recv(1024)
	if not answer_from_dict:
		idx = idx + 1
```

Googling was time consuming
