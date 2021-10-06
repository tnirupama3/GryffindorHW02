# GryffindorHW02
import pandas as pd
import sys
import csv

def convert_row(row,data):
      res="<player>\n"
      for i in range(1,len(data[0])):
        res+="\t<"+data[0][i]+">"+row[i]+"</"+data[0][i]+">\n"
      res+="</player>"
      return res

def convert_file(file_name, file_type):
    if file_type == 'c':
        csv_file = pd.read_csv(file_name,sep='\t',encoding='utf8')
        csv_file.to_csv('cmpe.csv')
    elif file_type == 'j':
        csv_file = pd.read_csv(file_name,sep='\t',encoding='utf8')
        csv_file.to_csv('cmpe.csv')
        csv_object = pd.read_csv('./cmpe.csv',encoding='utf8')
        csv_object.to_json('cmpe.json', orient='records', lines=True)
    elif file_type == 'x':
        csv_file = pd.read_csv(file_name,sep='\t',encoding='utf8')
        csv_file.to_csv('cmpe.csv')       
        f = open('cmpe.csv')
        csv_f = csv.reader(f)   
        data = []
        for row in csv_f: 
          data.append(row)
        f.close()
        with open('output.xml', 'w') as f: f.write('\n'.join([convert_row(row,data) for row in data[1:]]))



if (sys.argv[1] and sys.argv[2]):
    convert_file(sys.argv[1], sys.argv[2])
else:
    print('Please pass the valid params')
