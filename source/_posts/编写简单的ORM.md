---
title: ' 编写简单的ORM'
date: 2016-08-24 09:51:46
categories: "Python"
tags:
- 学习
---

最近在跟着廖雪峰的python3教程，把学习的过程记录下来。日后好反复翻阅
<!-- more -->

```python
class Field(object):
    def __init__(self, name, colum_type):
        self.name = name
        self.column_type = colum_type

    def __str__(self):
        return '<%s : %s>' % (self.__class__.__name__, self.name)


class StringField(Field):
    def __init__(self, name):
        super(StringField, self).__init__(name, 'varchar(100)')


class IntegerField(Field):
    def __init__(self, name):
        super(IntegerField, self).__init__(name, 'bigint')


class ModelMetaclass(type):
    def __new__(cls, name, bases, attrs):
        if name == 'Model':
            return type.__new__(cls, name, bases, attrs)
        print("Found model: %s" % name)
        mappings = dict()
        for k, v in attrs.items():
            if isinstance(v, Field):
                print("Found mapping: %s ==> %s" % (k, v))
                mappings[k] = v

        for k in mappings.keys():
            attrs.pop(k)

        attrs['__mappings__'] = mappings  # 保存属性和映射关系
        attrs['__table__'] = name  # 表明与类名一致
        return type.__new__(cls, name, bases, attrs)

class Model(dict, metaclass=ModelMetaclass):
    def __init__(self, **kw):
        super(Model, self).__init__(**kw)

    def __getattr__(self, key):
        try:
            return self[key]
        except KeyError:
            raise AttributeError(r"'Model' object has no attribute '%s' " % key)

    def __setattr__(self, key, value):
        self[key] = value

    def save(self):
        fields = []
        params = []
        args = []
        for k, v in self.__mappings__.items():
            fields.append(v.name)
            params.append("?")
            args.append(getattr(self, k, None))
        print('='.join(['name', 'iki']))
        sql = "INSERT INTO %s (%s) VALUES (%s)" % (self.__table__, ','.join(fields), ','.join(params))
        print('SQL: %s' % sql)
        print('ARGS: %s' % str(args))

    def update(self):
        pass



```

```python
class User(Model):
    # 定义类的属性到列的映射：
    id = IntegerField('id')
    name = StringField('username')
    email = StringField('email')
    password = StringField('password')

u = User(id=12345, name='Michael', email='test@orm.org', password='my-pwd')
u.save()

[OUTPUT]
Found model: User
Found mapping: id ==> <IntegerField : id>
Found mapping: name ==> <StringField : username>
Found mapping: email ==> <StringField : email>
Found mapping: password ==> <StringField : password>

SQL: INSERT INTO User (username,id,email,password) VALUES (?,?,?,?)
ARGS: ['Michael', 12345, 'test@orm.org', 'my-pwd']


```

**本段代码是照着廖雪峰python3教程敲得，后续会补充一些理解和扩展该代码**
