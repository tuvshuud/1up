### Misc 400 - LOL

I think they have changed category title between misc and programming. So it's programming challenge.

If you connect to given ip and port address, it asks you to send back decoded or decompressed value
to the server. Initially we thought it's 25 repititive tasks. But it's way more than that.
Challenge format is as follows 
```
Challenge score (0/25)
[challenge]-[decoded_text]
```

We wrote python script to get the flag.
```python
import socket, zlib, base64, time, string, binascii, codecs, bz2, brainfuck, subprocess
import traceback
solutions = {}
keywords = []

def solve_1(b64):
	return base64.b64decode(b64)

def solve_9(b32):
	return base64.b32decode(b32)

def solve_2(zl):
	return zl.decode('zlib')

def solve_3(input):
	b16 = input.strip()
	return base64.b16decode(b16)

def solve_4_2(input):
	longg = ['Do not wish it','Lead bye','Live each','Success is','Very little','I am a greater','If at first','If you try','It is better','It is hard','Luck is','No matter','Thank you','The difference','The most','The real','There are no', 'Your goals','Your smile']
        for l in longg:
				c = l
				c = c.replace(' ', '').lower()
				if input == solve_4(c):
					return l.strip('\n')

def solve_4(input):
	lstr = string.ascii_lowercase
        ustr = string.ascii_uppercase
        idx = 0
        result = list(input)
        for c in input:
                if c == ' ':
                        result[idx] = ' '
                elif c.isupper():
                        n = ustr.index(c)
                        result[idx] = ustr[(n + 16)%26]
                else:
                        n = lstr.index(c)
                        result[idx] = lstr[(n + 16)%26]
                idx = idx + 1
        return ''.join(result)

def solve_5(input):
	return input[::-1]

def solve_6(input):
	lstr = string.ascii_lowercase
	ustr = string.ascii_uppercase
	idx = 0
	result = list(input)
	for c in input:
		if c == ' ':
			result[idx] = ' '
		elif c.isupper():
			n = ustr.index(c)
			result[idx] = ustr[(n + 13)%26]
		else:
			n = lstr.index(c)
			result[idx] = lstr[(n + 13)%26]
		idx = idx + 1
	return ''.join(result)

def solve_7(input):
	n = int(input, 2)
	return binascii.unhexlify('%x' % n)

def solve_8(input):
	# return codecs.decode(input, "cp500")
	return input.decode('EBCDIC-CP-BE').encode('ascii')

def solve_10(input):
	return bz2.decompress(input)

def solve_11(input):
	f = open('temp.txt', 'w')
	f.write(input)
	f.close()
	return subprocess.check_output('python brainfuck.py temp.txt', shell=True)

def solve_12(input):
	return input.decode('hex')

solutions['ba64'] = solve_1
solutions['zlib'] = solve_2
solutions['ba16'] = solve_3
solutions['ro42'] = solve_4_2
solutions['revs'] = solve_5
solutions['roti'] = solve_6
solutions['bina'] = solve_7
solutions['ebcd'] = solve_8
solutions['ba32'] = solve_9
solutions['bz2c'] = solve_10
solutions['bfuk'] = solve_11
solutions['hexa'] = solve_12

s = socket.socket()
s.connect(('52.91.163.151', 30303))
print s.recv(1024)
print s.recv(1024)
i = 0
while True:
	try:
		# time.sleep(1)
		data = s.recv(1024)
		print "data %d {%s}" % (i, data.strip('\n'))
		data = '\n'.join(data.split('\n')[1:])
		challenge = data.split('-')[0]
		argument = '-'.join(data.split('-')[1:])
		argument = argument.strip('\n')
		# print "Challenge: %s-%s" % (challenge, argument)
		answer = solutions[challenge](argument)
		print "Answer: %s" % answer
		answer = answer.strip('\n')
		s.send(answer.encode())
		print s.recv(1024)
		print ''
		i = i + 1
	except Exception, ex:
		traceback.print_stack()
		print '--------------'
		traceback.print_exc()
		break
```

At 100th score, it gives the non task related string scramble. 
```
666p61677o6433633064696r675s69735s656173795s4p4s4p7q20
```
If you do rot13 and hex decode, we get the flag.
```
flag{d3c0ding_is_easy_LOL} 
```
