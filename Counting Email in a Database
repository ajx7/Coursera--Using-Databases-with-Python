import sqlite3

conn = sqlite3.connect('C:\\Users\Sony\emaildb.sqlite')
#create a database at some directory before commiting the above operation
cur = conn.cursor()

cur.execute('''
DROP TABLE IF EXISTS Counts''')

cur.execute('''
CREATE TABLE Counts (org TEXT, count INTEGER)''')

#save the file mbox.txt from the link provided in the desciption of the problem
fname = input('Enter file name: ')#Enter the dull link of the file 
if (len(fname) < 1): fname = 'mbox.txt'
fh = open(fname)
lst =[]
for line in fh:
    if not line.startswith('From: '): continue
    pieces = line.split()
    email = pieces[1]
    dom = email.find('@')
    org = email[dom+1:len(email)]

    cur.execute('SELECT count FROM Counts WHERE org = ? ', (org,))
    row = cur.fetchone()
    if row is None:
        cur.execute('''INSERT INTO Counts (org, count)
                VALUES (?, 1)''', (org,))
    else:
        cur.execute('UPDATE Counts SET count = count + 1 WHERE org = ?',
                    (org,))
conn.commit()
sqlstr = 'SELECT org, count FROM Counts ORDER BY count DESC LIMIT 10'

for row in cur.execute(sqlstr):
    print(str(row[0]), row[1])

#End of the program

cur.close()
