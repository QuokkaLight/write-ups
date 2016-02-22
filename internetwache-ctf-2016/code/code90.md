# Code90 - Dark Forest

## Description

Someone pre-ordered a forest and now I'm lost in it. There are a lot of binary trees in front and behind of me. Some are smaller or equal-sized than others. Can you help me to invert the path and find out of the forest? Hint: It's about (inverted) BSTs. Don't forget the spaces.

## Solution

This challenge was baset on Binary Search Trees.
We were given multiple list of numbers that we had to put in binary search trees.
Then we had to traverse the tree in postorder before reversing the resulting list.

The following Python code got us the flag.

```python
import re
import socket
import string

class tree(object):
	data = None
	left = None
	right = None
	count = 1

def postorder(tree):
	data = []

	def recurse(node):
		if not node:
			return
		recurse(node.left)
		recurse(node.right)
		for i in range(node.count):
			data.append(node.data)

	recurse(tree)
	return data

def get_tree(inline):
	t = tree()
	t1 = t

	for i in inline:
		t = t1
		while 1:
			if t.data is None:
				t.data = i
				break
			else:
				if i <= t.data:
					if t.left is None:
						t.left = tree()
					t = t.left
				elif t.data < i:
					if t.right is None:
						t.right = tree()
					t = t.right
				else:
					t.count += 1
					break

	return postorder(t1)

HOST = '188.166.133.53'
PORT = 11491       
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect((HOST, PORT))

data = s.recv(1024)

i = 0

while(data):
	print data

	if i == 0:
		m = re.search('\[(.*)\]', data)
		if m:
			s.send(m.group(0))
			i += 1
	else:
		m = re.search('\[(.*)\]', data)
		if m:
			nbr = m.group(1).split(',')
			# print nbr
			nbr = [int(i) for i in nbr]
			# print nbr
			nbr = [str(i) for i in reversed(get_tree(nbr))]
			nbr = '['+', '.join(nbr)+']'
			print nbr
			s.send(nbr)
	data = s.recv(1024)

s.close()

```