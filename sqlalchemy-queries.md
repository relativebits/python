### EQUALS:

query.filter(Language.name == 'python')

### NOT EQUALS:

query.filter(Language.name != 'python')

LIKE:

query.filter(Language.name.like('%py%'))

IN:

query.filter(Language.name.in_(['python', 'java', 'javascript']))

# works with query objects too:

query.filter(Language.name.in_(session.query(Language.name).filter(Language.name.like('%py%'))))

NOT IN:

query.filter(~Language.name.in_(['python', 'java', 'javascript']))

IS NULL:

filter(Language.name == None)

IS NOT NULL:

filter(Language.name != None)

AND:

from sqlalchemy import and_
filter(and_(Language.name == 'python', Language.version == '3.7'))

#or, default without and_ method comma separated list of conditions are AND

filter(Language.name == 'python', Language.version == '3.7')

# or call filter()/filter_by() multiple times

filter(Language.name == 'python').filter(User.version == '3.7')

OR:

from sqlalchemy import or_
filter(or_(Language.name == 'python', Language.name == 'java'))

match:

query.filter(Language.name.match('python'))
