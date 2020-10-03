## DRF Permissions

Before running the main body of the view each permission in the list is checked. If any permission check fails an `exceptions.PermissionDenied` or `exceptions.NotAuthenticated` exception will be raised, and the main body of the view will not run. When the permissions checks fail either a "403 Forbidden" or a "401 Unauthorized" response will be returned.

### Setting permission policy

    - Global settings:

        REST_FRAMEWORK = {
            'DEFAULT_PERMISSION_CLASSES': [
                'rest_framework.permissions.IsAuthenticated',
            ]
        }

        REST_FRAMEWORK = {
            'DEFAULT_PERMISSION_CLASSES': [
            'rest_framework.permissions.AllowAny',
            ]
        }

    - Classed-based view:

        from rest_framework.permissions import IsAuthenticated
        from rest_framework.response import Response
        from rest_framework.views import APIView

        class ExampleView(APIView):
            permission_classes = [IsAuthenticated]

            def get(self, request, format=None):
                content = {
                    'status': 'request was permitted'
                }
                return Response(content)


    - Function-based view:

        from rest_framework.decorators import api_view, permission_classes
        from rest_framework.permissions import IsAuthenticated
        from rest_framework.response import Response

        @api_view(['GET'])
        @permission_classes([IsAuthenticated])
        def example_view(request, format=None):
            content = {
                'status': 'request was permitted'
            }
            return Response(content)

### Most common permissions

`AllowAny` - will allow unrestricted access, regardless of if the request was authenticated or unauthenticated (Not required as it's the default behavior. Still, good practice to explicitly specify)

`IsAuthenticated` - will deny permission to any unauthenticated user, and allow permission otherwise.

`IsAdminUser` - will deny permission to any user, unless user.is_staff is True in which case permission will be allowed.

`IsAuthenticatedOrReadOnly` - will allow authenticated users to perform any request. Requests for unauthorized users will only be permitted if the request method is one of the "safe" methods; GET, HEAD or OPTIONS.

[Go back](../README.md)
