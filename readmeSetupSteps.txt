
rmvirtualenv djangoenv			;***MMM only if already exists
mkvirtualenv djangoenv
pip install django==2.1.5		;***MMM DO NOT USE 2.1.1 THROWS EXCEPTIONS

django-admin help
django-admin startproject mysite
cd mysite
python manage.py runserver		; start django
open a browser url = localhost:8000	; test
python manage.py migrate		; create the database (see section in mysite\settings.py)
dir					; note the db.sqlite3 db is created
winpty python manage.py createsuperuser		; create a superuser to admin the db
	user = mike
	password = Password1!
python manage.py startapp polling	; create a polling app
dir					; note the polling created app folder
edit mysite\settings
	section: INSTALL_APPS
			add your polling app to the bottom of the list
			'polling',	; ***MMM be sure to include the single quotes
git init
			
create the overall site web templates
mkdir mysite\templates
edit mysite\templates\base.html		; ref the video for the code
edit mysite\settings.py			; add 'DIRS': [os.path.join(BASE_DIR, 'mysite/templates')],        

edit mysite\polling\models.py		; ref the video
python manage.py makemigrations		; migrate the changes to the db
python manage.py migrate
edit mysite\polling\admin.py		; register the poll model
start python manage.py runserver	;  # Then visit http://localhost:8000/admin/
mkdir mysite\polling\templates\polling	; we create polling view templates under our polling app
edit mysite\polling\templates\polling\list.html		; create template, ref the video
edit mysite\polling\templates\polling\detail.html	; create template, ref the video
edit mysite\polling\views.py		; add the view for the template, ref the video
edit mysite\urls.py			; define the route to your top level site in urlpatterns, see the video
edit mysite\polling\urls.py		; routes for the polling app
start python manage.py runserver	;  # Then visit http://localhost:8000/polling/

python manage.py startapp blogging	; create the blogging app
edit mysite\settings
	section: INSTALL_APPS
			add your polling app to the bottom of the list
			'blogging',	; ***MMM be sure to include the single quotes
python manage.py makemigrations blogging	; migrate the table changes to the db for blogging
python manage.py migrate			; update the db

- using the django shell to test interactively
python manage.py shell
from blogging.models import Post
from django.contrib.auth.models import User
all_users = User.objects.all()
p2 = Post(title="Another post",
            text="The second one created",
            author=all_users[0]).save()
p3 = Post(title="The third one",
            text="With the word 'heffalump'",
            author=all_users[0]).save()
p4 = Post(title="Posters are a great decoration",
            text="When you are a poor college student",
            author=all_users[0]).save()
Post.objects.count()

- the blogging app via admin
edit mysite\blogging\admin.py		; ref the video
python manage.py runserver		; start django












