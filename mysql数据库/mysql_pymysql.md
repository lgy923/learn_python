



```mysql
import pymysql


def my_sql(sql):
    connection = pymysql.connect(
        host='127.0.0.1',
        user='root',
        password='12345678',
        db='gongsi',
        charset='utf8',
        cursorclass=pymysql.cursors.DictCursor
    )

    with connection.cursor() as cursor:
        # sql = "select * from `Employee`"
        cursor.execute(sql)
        data = cursor.fetchall()

    return data


if __name__ == '__main__':
    sql = "select * from `Employee`"
    result = my_sql(sql)
    print(result)
```





```mysql
import pymysql


def my_sql(sql):
    connection = pymysql.connect(
        host='127.0.0.1',
        user='root',
        password='12345678',
        db='gongsi',
        charset='utf8',
        cursorclass=pymysql.cursors.DictCursor
    )

    with connection.cursor() as cursor:
        # sql = "select * from `Employee`"
        cursor.execute(sql)
        data = cursor.fetchall()

    return data


if __name__ == '__main__':
    while True:
        sql = input(">>>")

        if sql == 'exit':
            break

        result = my_sql(sql)
        print(result)
```



```mysql
from sqlalchemy import create_engine
from sqlalchemy.ext.declarative import declarative_base

from sqlalchemy import Column, Integer, String

from sqlalchemy.orm import sessionmaker

# 用户名：密码@地址/数据库名
engine = create_engine('mysql+pymysql://root:12345678@127.0.0.1/gongsi', echo=True)
Base = declarative_base()


class User(Base):
    __tablename__ = 'al_user'  # 创建的数据库名
    id = Column(Integer, primary_key=True)
    name = Column(String(255))
    fullname = Column(String(255))
    nickname = Column(String(200))


# Base.metadata.create_all(engine)

Session = sessionmaker(bind=engine)
session = Session()

ed_user = User(name='西川结衣', fullname='西川', nickname='结衣')

session.add(ed_user)
session.commit()
```



