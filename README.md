# django-channels-demo

# Requirements

install requirements.txt for all requirements using command pip install -r requirements.txt

# Working

here mysite is our django project and chat is our application.

starting with mysite/settings.py 
add your 'app name' and 'channels' to installed apps

add your prefered database details

add ASGI_APPLICATION = 'mysite.asgi.application'

add 

 CHANNEL_LAYERS = {
    'default': {
        'BACKEND': 'channels_redis.core.RedisChannelLayer',
        'CONFIG': {
            "hosts": [('127.0.0.1', 6379)],
        },
    },
}

-- Now as channels are for real time data and websockets we need to configyre the asgi.py file and for that mysite/asgi.py.

for routing add the websocket urlpattern as in the chat/routing.py

for handshake to occur (for our requests) we write the code as per chat/consumers.py.

here we had used Asynchronous websocket which means multiple requests occur in parallel and if we want single request , synchronous method should be used .

in this code (consumers.py) we had async def ... which reflects the asynchronous method and await is just like yield and return which is written when async is used.


Now for templates to show the output we had made two templates as templates/chat/index.html and templates/chat/room.html.

we had rendered the templates in chat/views.py

Add necessary urls in chat/urls.py and include it in mysite/urls.py.

# to see the output

python manage.py makemigrations

pyhton manage.py migrate

python manage.py runserver

for output to be seen activate you redis server using command redis-server

http://127.0.0.1:8000/chat

it asks for room name , enter that

http://127.0.0.1:8000/chat/hi

it opens the room where the data you write will reflect in room . 

