# ronnin_site

pip install djangorestframework
develop branch
mkdir src
cd src
django-admin startproject ronnin-site .
cd ronnin-site
python manage.py startapp users
code .
cntrl shift p > select python interpreter
open terminal in vscode

>settings.py
add to INSTALLED_APPS at the end  

'rest_framework',
'rest_framework.authtoken',

'users'




>models.py

from django.contrib.auth.models import AbstractUser

class CustomUser(AbstractUser):
    pass

>settings.py

at the end
AUTH_USER_MODEL = "users.CustomUser"

moify this
LANGUAGE_CODE = 'es-co'
TIME_ZONE = 'America/Bogota'

>admin.py

from django.contrib import admin
from django.contrib.auth.admin import UserAdmin
from users.models import CustomUser

class CustomUserAdmin(UserAdmin):
    # add_form = "esto es para adicionar nuevos campos"
    # form = 
    model = CustomUser
    list_display = ["username","email", "is_staff"]

admin.site.register(CustomUser,CustomUserAdmin)

>console
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser

pip install django-rest-auth django-allauth django-registration django-crispy-forms

>settings.py

'django.contri.sites',
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

from django.urls import path, include

    path("accounts/", include("django.contrib.auth.urls")),
    path("api-auth/", include("rest_framework.urls")),
    path("api/rest-auth", include("rest_auth.urls")),
    path("api/rest-auth/registration", include("rest_auth.registration.urls")),

create users/forms.py
>forms.py
from django_registration.forms import RegistrationForm
from users.models import CustomUser

class CustomeUserForm(RegistrationForm):
    class Meta(RegistrationForm.Meta):
        model = CustomUser

>urls.py
from django_registration.backends.one_step.views import RegistrationView
from users.forms import CustomeUserForm

    path("accounts/", include("django_registration.backends.one_step.urls")),
    #login user
    path("accounts/", include("django.contrib.auth.urls")),
    #login web restapi
    path("api-auth/", include("rest_framework.urls")),
    #login restapi
    path("api/rest-auth", include("rest_auth.urls")),
    #register restapi
    path("api/rest-auth/registration", include("rest_auth.registration.urls")),

>settings.py

LOGIN_URL = "accounts/login"
LOGIN_REDIRECT_URL="/"
LOGOUT_REDIRECT_URL="/"
# Static files (CSS, JavaScript, Images)

modify TEMPLATES 

'DIRS': [os.path.join(BASE_DIR, 'templates')]

Create src/templates/django_registration folder
Create src/templates/registration folder
Create src/templates/auth_layout.html file