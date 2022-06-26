# Reading and Writing files using os
```jupyter
import os
from urllib.request import urlretrieve

urls =['https://gist.githubusercontent.com/aakashns/257f6e6c8719c17d0e498ea287d1a386/raw/7def9ef4234ddf0bc82f855ad67dac8b971852ef/loans1.txt',
'https://gist.githubusercontent.com/aakashns/257f6e6c8719c17d0e498ea287d1a386/raw/7def9ef4234ddf0bc82f855ad67dac8b971852ef/loans2.txt',
'https://gist.githubusercontent.com/aakashns/257f6e6c8719c17d0e498ea287d1a386/raw/7def9ef4234ddf0bc82f855ad67dac8b971852ef/loans3.txt']

os.makedirs('./data', exist_ok=True)

i = 1
for url in urls:
	urlretrieve(url, './data/loans'+ str(i) +'.txt')
	i += 1


def parse_header(header_line):
	return header_line.strip().split(',')
	
def parse_content(content):
	parsed_content = []
	for line in content:
		current = []
		
		for val in line.strip().split(','):
			current.append(float(val) if val != '' else 0.0)
			
		parsed_content.append(current)
		
	return parsed_content

files = os.listdir('./data')

data = []

for file in files:
	with open('./data/' + file, mode='r') as f:
		f_lines = f.readlines()
		header = parse_header(f_lines[0])
		content = parse_content(f_lines[1:])
		if len(data) < 1:
			data.append(header)
		for c in content:
			data.append(c)


print(data)


		

```