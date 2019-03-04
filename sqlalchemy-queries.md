```
from sqlalchemy import Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class Language(Base):
    __tablename__ = 'language'
    id = Column(Integer, primary_key=True)
    name =  Column(String(50))
    version =  Column(String(50))
```

### EQUALS
```
Language.query.filter(Language.name == 'python')
```

### NOT EQUALS
```
Language.query.filter(Language.name != 'python')
```

### LIKE
```
Language.query.filter(Language.name.like('%py%'))
```

### IN
```
Language.query.filter(Language.name.in_(['python', 'java', 'javascript']))

Language.query.filter(Language.name.in_(session.query(Language.name).filter(Language.name.like('%py%'))))
```

### NOT IN
```
Language.query.filter(~Language.name.in_(['python', 'java', 'javascript']))
```

### IS NULL
```
Language.filter(Language.name == None)
```

### IS NOT NULL
```
Language.filter(Language.name != None)
```

### AND
```
from sqlalchemy import and_
Language.filter(and_(Language.name == 'python', Language.version == '3.7'))

#or, default without and_ method comma separated list of conditions are AND

Language.filter(Language.name == 'python', Language.version == '3.7')
```

### OR
```
from sqlalchemy import or_
Language.filter(or_(Language.name == 'python', Language.name == 'java'))
```

### MULTIPLE FILTERING
```
Language.filter(Language.name == 'python').filter(User.version == '3.7')
```

### MATCH
```
Language.query.filter(Language.name.match('python'))
```

### RANDOM RECORD SELECTION
```
Language.query(Language).order_by(func.rand()).first()

Language.query.filter(Language.version.like("%3%")).order_by(func.rand()).first()
```
