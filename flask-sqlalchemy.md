
# Abstract Model
Example of an abstract sqlalchemy model using the flask-sqlalchemy extension. This allows concrete models to extend the abstract model and inherit common columns needed by all models (e.g. created_on and modified_on timestamps).

```
class AbstractModel(db.Model):
    __abstract__ = True
    created_on = db.Column(db.DateTime, default=db.func.current_timestamp(), nullable=False)
    modified_on = db.Column(db.DateTime, default=db.func.current_timestamp(), onupdate=db.func.current_timestamp(),
                            nullable=False)

    @property
    def columns(self):
        return [c.name for c in self.__table__.columns]

    @property
    def column_values(self):
        return dict([(c, getattr(self, c)) for c in self.columns])

    def as_dict(self):
        return self.column_values

    def __repr__(self):
        return '{}({})'.format(self.__class__.__name__, self.column_values)

    def __str__(self):
        return '{}({})'.format(self.__class__.__name__, self.column_values)
```        
