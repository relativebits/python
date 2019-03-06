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
session.query(Language).filter(Language.name == 'python')
```

### NOT EQUALS
```
session.query(Language).filter(Language.name != 'python')
```

### LIKE
```
session.query(Language).filter(Language.name.like('%py%'))
```

### IN
```
session.query(Language).filter(Language.name.in_(['python', 'java', 'javascript']))

session.query(Language).filter(Language.name.in_(session.query(Language.name).filter(Language.name.like('%py%'))))
```

### NOT IN
```
session.query(Language).filter(~Language.name.in_(['python', 'java', 'javascript']))
```

### IS NULL
```
session.query(Language).filter(Language.name == None)
```

### IS NOT NULL
```
session.query(Language).filter(Language.name != None)
```

### AND
```
from sqlalchemy import and_
session.query(Language).filter(and_(Language.name == 'python', Language.version == '3.7'))

#or, default without and_ method comma separated list of conditions are AND

session.query(Language).filter(Language.name == 'python', Language.version == '3.7')
```

### OR
```
from sqlalchemy import or_
session.query(Language).filter(or_(Language.name == 'python', Language.name == 'java'))
```

### MULTIPLE FILTERING
```
session.query(Language).filter(Language.name == 'python').filter(User.version == '3.7')
```

### MATCH
```
session.query(Language).query.filter(Language.name.match('python'))
```

### RANDOM RECORD SELECTION
```
session.query(Language).order_by(func.rand()).first()

session.query.filter(Language.version.like("%3%")).order_by(func.rand()).first()
```
