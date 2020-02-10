2020-02-04-Creating Django models of an existing DB





## 1. django에서 이미 생성된 DB에따라 model 자동 생성하기.

### Creating Django models of an existing DB





보통 관계형 데이터베이스를 만들때, 모델링 프로그램을 먼저 돌려서 db에 테이블들을 만들어 놓는다. 이때, 나는 이 db를 토대로 손쉽게 간편하게 django의 models.py를 만들어주는 방법이 없을까 하는 생각이 들었다. 

> 본디 프로그래밍은 불편한것을 누군가 항상 해결해 놓았다!



```
python manage.py inspectdb
```



이 명령어를 쓴다면, 연결해 놓은 DB를 들여다보며 자동으로 코딩으로 되돌려준다. 



```python
python manage.py inspectdb
# This is an auto-generated Django model module.
# You'll have to do the following manually to clean this up:
#   * Rearrange models' order
#   * Make sure each model has one field with primary_key=True
#   * Make sure each ForeignKey has `on_delete` set to the desired behavior.
#   * Remove `managed = False` lines if you wish to allow Django to create, modify, and delete the table
# Feel free to rename the models, but don't rename db_table values or field names.
from django.db import models


class AuthGroup(models.Model):
    name = models.CharField(unique=True, max_length=150)

    class Meta:
        managed = False
        db_table = 'auth_group'
        .
        .
        .
```

이때, class Meta 안에 있는 managed 속성을 True로 바꾸거나 지워야지 migrate를 할때 적용된다. 

자동으로 불러와도 안타깝게도 완벽하게 불러오지는 않는다. 코드 입력시 꼭 속성들을 살펴보자.





- class Meta의 manged 

manged 속성은 False일때 더이상 이 테이블은 DB에 반영하지 않겠다라는 뜻. 











참고: https://dev.to/idrisrampurawala/creating-django-models-of-an-existing-db-288m

