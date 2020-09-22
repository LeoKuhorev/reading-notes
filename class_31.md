## Docker Intro

Docker _**image**_ is a snapshot in time of what a project contains.  
A _**container**_ is a running instance of the image.  
_**docker-compose.yml**_ - is a list of container instructions.

- `docker --version` - check Docker version;
- `docker-compose --version` - check Docker-compose version;
- `docker info` - get info about Docker;
- `docker image ls` - inspect current image;
- `docker container ls -la` - inspect current container;
- `docker image build .` - build the image;
- `docker-compose up --build` - build the image and run the container;

### Dockerfile

_**Dockerfile**_ contains all the requirements for the container (analogue of Pipenv).
Dockerfiles are read from top-to-bottom. The first instruction must be the `FROM` command which lets us import a base image to use for our image. This base image could be another Docker image or one we create entirely from scratch.

    # Dockerfile
    FROM python:3.7-alpine

## DRF

- create a new app
- install DRF
- configure project-level and app-level urls.py

        from django.urls import path
        from .views import BookAPIView

        urlpatterns = [
            path('', BookAPIView.as_view()),
        ]

- configure views.py

        from rest_framework import generics

        from books.models import Book
        from .serializers import BookSerializer


        class BookAPIView(generics.ListAPIView):
            queryset = Book.objects.all()
            serializer_class = BookSerializer

- create serializers.py
  from rest_framework import serializers

        from books.models import Book


        class BookSerializer(serializers.ModelSerializer):
            class Meta:
                model = Book
                fields = ('title', 'subtitle', 'author', 'isbn')

[Go back](./README.md)
