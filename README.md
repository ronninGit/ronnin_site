# ronnin_site
this is the main site

mkdir src
django-admin startproject ronnin-site .
cd ronnin-site
python manage.py startapp users
code .
cntrl shift p > select python interpreter
open terminal in vscode
add to INSTALLED_APPS at the end  

'rest_framework',
'rest_framework.authtoken',

'users'




>models.py

from django.contrib.auth.models import AbstracUser

class CustomUser(AbstractUser):
    pass

>settings.py

at the end
AUTH_USER_MODEL = "users.CustomUser"

LANGUAGE_CODE = 'es-co'
TIME_ZONE = 'America/Bogota'

>admin.py

from django.contrib import admin
from django.contrib.auth.admin import UserAdmin
from user.models import CustomUser

class CustomUserAdmin(UserAdmin):
    # add_form = "esto es para adicionar nuevos campos"
    # form = 
    model = CustomUser
    list_display = ["username","email", "is"]

admin.site.register(CustomUser,CustomUserAdmin)

>console
python manage.py makemigrations
python manage.py createsuperuser

pip install django-rest-auth
pip install django-allauth
pip install django-registration
pip install django-crispy-forms

>settings.py

'django.contri.sites,
'allauth',
'allauth.account',
'allauth.socialaccount',
'rest_auth',
'rest_auth.registration',
'crispy_forms',

at the end

CRISPY_TEMPLATE_PACK = "boostrap4"
#django.contrib.sites
SITE_ID = 1
#django-allauth
ACCOUNT_EMAIL_VERIFICATION = "none"
ACCOUNT_EMAIL_REQUIRED = (True)

>console
python  manage.py migrate

>urls.py

add to urlpatterns

path("api-auth/", incude("rest_framework.urls")),
path("api/rest-auth", incude("rest_auth.urls")),
path("api/rest-auth/registration", incude("rest_auth.registration.urls")),