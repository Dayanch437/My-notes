~~~python
@admin.register(AdmissionStaff)

class AdmissionStaff(admin.ModelAdmin):

list_display = ['id','staff','place']

  
  

from django.contrib import admin

from .models import AdmissionExamDateRegion, AdmissionExam, AdmissionSubject

from apps.regions.models import Region

  
  

@admin.register(AdmissionExamDateRegion)

class AdmissionExamDateRegionAdmin(admin.ModelAdmin):

	list_display = ['admission_exam', 'subject', 'region', 'date_of_exam']

list_filter = ['admission_exam', 'subject', 'region', 'date_of_exam']

search_fields = [

'admission_exam__name',

'subject__name',

'region__name'

]

autocomplete_fields = ['admission_exam', 'subject', 'region']
~~~
