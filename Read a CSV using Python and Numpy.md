# Read a CSV using Python and Numpy
First of all you get your data file in [[CSV]], in this case we will get it from downloading it from the internet using urllib:

	import urllib.request
	urllib.request.urlretrive('www.url.com/data.csv', 'data.txt')

After that we simply use numpy to get the data into an array with the command *np.genfromtxt*:

	import numpy as np
	data = np.genfromtxt('data.txt', delimiter=',', skip_header=1)

