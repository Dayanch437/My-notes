
~~~python 

class StudentViewSet(viewsets.ModelViewSet):
    serializer_class = StudentSerializer

    def get_queryset(self):
        user = self.request.user

        # Check if the user belongs to the 'SuperAdmin' group
        if user.groups.filter(name='SuperAdmin').exists():
            return Student.objects.all()

        # Check if the user belongs to the 'province_admin' group
        elif user.groups.filter(name='province_admin').exists():
            return Student.objects.filter(
                education_center__region=user.region
            )

        # Check if the user belongs to the 'edu_center_admin' group
        elif user.groups.filter(name='edu_center_admin').exists():
            return Student.objects.filter(
                education_center=user.education_center
            )

        # If the user doesn't match any of the above, return an empty queryset
        return Student.objects.none()

    def perform_create(self, serializer):
        user = self.request.user

        # If the user is an 'edu_center_admin', automatically assign the education center
        if user.groups.filter(name='edu_center_admin').exists():
            serializer.save(education_center=user.education_center)
        else:
            serializer.save()

~~~

