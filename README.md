# UbuntuDjango_beautyClinicApp

1.在分支master下初始化django项目beautyClinicApp，并将代码推送至远程库；
2.创建新分支createApp，并完成代码
    1）在pycharm下打开项目beautyClinicApp,在Tools栏打开run manage.py 命令窗，执行startapp manager命令
       在beautyClinicApp下创建一个app managers,并将app managers到settings文件里INSTALLED_APPS下注册，
       'managers.apps.AppConfig'。
3.在app managers下的models.py文件里，编写”表“结构。
    class Department(models.Model):
        """部门表"""
        title = models.CharField(verbose_name="标题", max_length=32)


    class UserInfo(models.Model):
        """员工表"""
        name = models.CharField(verbose_name="姓名", max_length=16)
        password = models.CharField(verbose_name="密码", max_length=64)
        age = models.IntegerField(verbose_name="年龄")
        account_balances = models.DecimalField(verbose_name="账户余额", max_length=10, decimal_places=2, default=0)
        entry_time = models.DateTimeField(verbose_name="入职时间")
        department = models.ForeignKey(verbose_name="所属部门", to="Department", null=True, blank=True, to_field="id",
                                       on_delete=models.SET_NULL)
    
        gender_choices = ((1, "男"), (2, "女"),)
        gender = models.SmallIntegerField(verbose_name="性别", choices=gender_choices)
4.在远程数据库中创建beautyClinic数据库
    1）访问远程服务器   ssh root@47.92.30.203
    2）root用户访问MYSQL   mysql -uroot -pxxxxxxxxxx
    3) 创建一个项目数据库beautyClinicDB   create database beautyClinicDB;
    4) 创建一个可用密码（88888888）访问的来自任意IP（%）的远程用户（remoteUser）    CREATE USER 'remoteser'@'%' IDENTIFIED BY '88888888';
    5) 修改远程用户对beautyClinicDB数据库的权限，使其能对该数据库有任意操作权限 grant all privileges on beautyClinicDB.*  to remoteUser@'%';
5.在项目下settings.py文件下DATABASES里设置项目数据库参数
    DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'beautyClinicDB',
        'USER': 'remoteUser',
        'PASSWORD': '88888888',
        'HOST': '47.92.30.203',
        'PORT': 3306,
       }
    }
6.通过django命令生成项目数据库内容 
    python3 manage.py makemigrations
    python3 manage.py migrate
    或者在pycharm的tools栏运行manage.py窗，执行makemigrations和 migrate命令