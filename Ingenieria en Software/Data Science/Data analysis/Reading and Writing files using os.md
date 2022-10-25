```jupyter
import os
from urllib.request import urlretrieve
import math

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
	
def parse_line(line):
	parsed_line = []
	for val in line.strip().split(','):
		parsed_line.append(float(val) if val != '' else 0.0)
				
	return parsed_line

def creat_dict(values, headers):
	result = {}
	for value, header in zip(values, headers):
		result[header] = value
	return result

def parse_CSV(path):
	data = []
	with open(path, mode='r') as f:
		f_lines = f.readlines()
		header = parse_header(f_lines[0])
		for line in f_lines[1:]:
			values = parse_line(line)
			data.append(creat_dict(values, header))
	return data

def loan_emi(amount, duration, rate, down_payment=0):
    """Calculates the equal montly installment (EMI) for a loan.
    
    Arguments:
        amount - Total amount to be spent (loan + down payment)
        duration - Duration of the loan (in months)
        rate - Rate of interest (monthly)
        down_payment (optional) - Optional intial payment (deducted from amount)
    """
    loan_amount = amount - down_payment
    try:
        emi = loan_amount * rate * ((1+rate)**duration) / (((1+rate)**duration)-1)
    except ZeroDivisionError:
        emi = loan_amount / duration
    emi = math.ceil(emi)
    return emi

def compute_emi(loans):
	for loan in loans:
		loan['emi'] = loan_emi(loan['amount'], loan['duration'], loan['rate'] / 12, loan['down_payment'])

def write_csv(data, path):
	with open(path, mode='w') as f:
		if len(data) == 0:
			return 
		
		headers = list(data[0].keys())
		f.write(','.join(headers) + '\n')
		
		for item in data:
			values = []
			for header in headers:
				values.append(str(item.get(header,'')))
			f.write(','.join(values) + '\n')
		

files = os.listdir('./data')

print('Processing...')

for i in range (1, 4):
	loans = parse_CSV('./data/loans{}.txt'.format(i))
	compute_emi(loans)
	write_csv(loans, './data/emi{}.txt'.format(i))

print('Done.')
		

```