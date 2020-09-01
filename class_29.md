## Django Custom User Model

The easiest way to create a custom user is to do it the very first thing in a new app (before running migrations). It takes five steps:

- create 'users' app
- update settings.py

        INSTALLED_APPS = [
        'users.apps.UsersConfig',
        ]

        AUTH_USER_MODEL = 'users.CustomUser'

- create a new CustomUser model

        from django.contrib.auth.models import AbstractUser
        from django.db import models

        class CustomUser(AbstractUser):
            pass
            # add additional fields in here

            def __str__(self):
                return self.username

- create new UserCreation and UserChangeForm

        from django import forms
        from django.contrib.auth.forms import UserCreationForm, UserChangeForm
        from .models import CustomUser

        class CustomUserCreationForm(UserCreationForm):

            class Meta:
                model = CustomUser
                fields = ('username', 'email')

        class CustomUserChangeForm(UserChangeForm):

            class Meta:
                model = CustomUser
                fields = ('username', 'email')

- update the admin

        from django.contrib import admin
        from django.contrib.auth import get_user_model
        from django.contrib.auth.admin import UserAdmin

        from .forms import CustomUserCreationForm, CustomUserChangeForm
        from .models import CustomUser

        class CustomUserAdmin(UserAdmin):
            add_form = CustomUserCreationForm
            form = CustomUserChangeForm
            model = CustomUser
            list_display = ['email', 'username',]

        admin.site.register(CustomUser, CustomUserAdmin)

If the migrations were already run, one can modify the standart User model by adding extra model (e.g. Profile), creating OneToOne relation with the User model, and creating signals.py with something like that:

    from django.db.models.signals import post_save
    from django.contrib.auth.models import User
    from django.dispatch import receiver
    from .models import Profile


    @receiver(post_save, sender=User)
    def create_profile(sender, instance, created, **kwargs):
        if created:
            Profile.objects.create(user=instance)

    @receiver(post_save, sender=User)
    def save_profile(sender, instance, **kwargs):
        instance.profile.save()

At the same time you need to extend AppConfig class with the ready() function:

    class UsersConfig(AppConfig):
    name = 'users'

    def ready(self):
        import users.signals

[Go back](./README.md)
