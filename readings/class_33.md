## JWT Intro

_**JSON Web Token (JWT)**_ is an open standard that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed.

In its compact form, JSON Web Tokens consist of three parts separated by dots (.), which are:

- **Header** - typically consists of two parts: the type of the token, which is JWT, and the signing algorithm being used, such as HMAC SHA256 or RSA.

  For example:

        {
        "alg": "HS256",
        "typ": "JWT"
        }

- **Payload** - contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims: registered, public, and private claims.

  For example:

        {
        "sub": "1234567890",
        "name": "John Doe",
        "admin": true
        }

- **Signature** - to create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

Therefore, a JWT typically looks like the following:

(header.payload.signature)
<img src="./assets/encoded-jwt.png" style="width:80%">

Whenever the user wants to access a protected route or resource, the user agent should send the JWT, typically in the Authorization header using the Bearer schema. The content of the header should look like the following: `Authorization: Bearer <token>`

The JWT is acquired by exchanging an username + password for an _**access token**_ and an _**refresh token**_. The _**access token**_ is usually short-lived (expires in 5 min or so, can be customized though).

The _**refresh token**_ lives a little bit longer (expires in 24 hours, also customizable). It is comparable to an authentication session. After it expires, you need a full login with username + password again.

## Using JWT in DRF

- install `pip install djangorestframework_simplejwt`
- add to settings.py

        REST_FRAMEWORK = {
            'DEFAULT_AUTHENTICATION_CLASSES': [
                'rest_framework_simplejwt.authentication.JWTAuthentication',
            ],
        }

- add to urls.py

          from django.urls import path
          from rest_framework_simplejwt import views as jwt_views

          urlpatterns = [
              # Your URLs...
              path('api/token/', jwt_views.TokenObtainPairView.as_view(), name='token_obtain_pair'),
              path('api/token/refresh/', jwt_views.TokenRefreshView.as_view(), name='token_refresh'),
          ]

- example app views.py

        from rest_framework.views import APIView
        from rest_framework.response import Response
        from rest_framework.permissions import IsAuthenticated


        class HelloView(APIView):
            permission_classes = (IsAuthenticated,)

            def get(self, request):
                content = {'message': 'Hello, World!'}
                return Response(content)

- example app urls.py

        from django.urls import path
        from myapi.core import views

        urlpatterns = [
            path('hello/', views.HelloView.as_view(), name='hello'),
        ]

## Usage

- authenticate and obtain the token. The endpoint is /api/token/ and it only accepts POST requests.

`http post http://127.0.0.1:8000/api/token/ username=vitor password=123`

- So basically your response body is the two tokens:

          {
              "access": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQ1MjI0MjU5LCJqdGkiOiIyYmQ1NjI3MmIzYjI0YjNmOGI1MjJlNThjMzdjMTdlMSIsInVzZXJfaWQiOjF9.D92tTuVi_YcNkJtiLGHtcn6tBcxLCBxz9FKD3qzhUg8",
              "refresh": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTU0NTMxMDM1OSwianRpIjoiMjk2ZDc1ZDA3Nzc2NDE0ZjkxYjhiOTY4MzI4NGRmOTUiLCJ1c2VyX2lkIjoxfQ.rA-mnGRg71NEW_ga0sJoaMODS5ABjE5HnxJDb0F8xAo"
          }

- After that you are going to store both the access token and the refresh token on the client side, usually in the `localStorage`
- In order to access the protected views on the backend (i.e., the API endpoints that require authentication), you should include the access token in the header of all requests (You can use this access token for the next five minutes)
- To get a new access token, you should use the refresh token endpoint /api/token/refresh/ posting the refresh token:

`http post http://127.0.0.1:8000/api/token/refresh/ refresh=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJ0b2tlbl90eXBlIjoicmVmcmVzaCIsImV4cCI6MTU0NTMwODIyMiwianRpIjoiNzAyOGFlNjc0ZTdjNDZlMDlmMzUwYjg3MjU1NGUxODQiLCJ1c2VyX2lkIjoxfQ.Md8AO3dDrQBvWYWeZsd_A1J39z6b6HEwWIUZ7ilOiPE`

[Go back](../README.md)
