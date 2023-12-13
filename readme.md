
1. **Создайте Django-проект:**
   
   В вашем терминале выполните следующие команды:

   ```bash
   django-admin startproject config
   ```

2. **Создайте приложения `ManytoMany`:**
   
   ```bash
   python3 manage.py startapp ManytoMany
   ```

3. **Определите модель Student:**

   ```python
   class Student(models.Model):
        first_name = models.CharField(max_length=50)
        last_name = models.CharField(max_length=50)
        email = models.EmailField()
        age = models.IntegerField()
        created_at = models.DateTimeField(auto_now_add=True)
        update_at = models.DateTimeField(auto_now=True)

        def __str__(self) -> str:
            return f'{self.first_name} -> {self.last_name}'
   ```

4. **Определите модель Course:**

   ```python
  class Course(models.Model):
        name = models.CharField(max_length=100)
        description = models.TextField()
        students = models.ManyToManyField(Student, related_name='courses')

        def __str__(self) -> str:
            return f'{self.name}'

   ```

5. **Настройте приложения в `settings.py`:**

   В файле `config/settings.py` добавьте в раздел `INSTALLED_APPS` ваши приложения:

   ```python
   INSTALLED_APPS = [
       # ...
        'rest_framework',
        'ManytoManyApp'
   ]
   ```

6. **Выполните миграции:**

   ```bash
   python manage.py makemigrations
   python manage.py migrate
   ```