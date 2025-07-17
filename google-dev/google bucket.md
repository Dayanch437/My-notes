1. **Install Required Packages**

~~~bash 
pip install django-storages google-cloud-storage
~~~

### 2. **Enable APIs & Create Service Account**

- Go to Google Cloud Console.
    
- Enable **"Cloud Storage"** API.
    
- Create a **Service Account** with the role `Storage Admin`.
    
- Generate a **JSON key** and download it.

### 3. **Create a GCS Bucket**

- Go to **Storage** → **Create Bucket**
    
- Name it (e.g., `my-django-media`)
    
- Make it public or use signed URLs if needed.


4. **Configure `settings.py`**
~~~bash
import os
from google.oauth2 import service_account

INSTALLED_APPS [
	"storages", #add this line
]
DEFAULT_FILE_STORAGE = 'storages.backends.gcloud.GoogleCloudStorage'  
GS_BUCKET_NAME = 'dayanch'  
GS_PROJECT_ID = 'protean-cove-461409-h3'  
GS_CREDENTIALS = service_account.Credentials.from_service_account_file(  
    os.path.join(BASE_DIR, 'credentials.json'),  
    scopes=['https://www.googleapis.com/auth/cloud-platform']  
)  
GS_DEFAULT_ACL = 'publicRead'  # Or 'private' for non-public files  
GS_BLOB_CHUNK_SIZE = 1024 * 256  # 256KB chunk size  
GS_QUERYSTRING_AUTH = False  
# Media files configuration  
MEDIA_URL = 'https://storage.googleapis.com/{}/'.format(GS_BUCKET_NAME)  
MEDIA_ROOT = ''  
  
STATIC_URL = '/static/'  
STATIC_ROOT = BASE_DIR / 'assets'  
  
STORAGES = {  
    "default": {  
        "BACKEND": "storages.backends.gcloud.GoogleCloudStorage",  
    },  
    "staticfiles": {  
        "BACKEND": "django.contrib.staticfiles.storage.StaticFilesStorage",  
    },  
}
			
~~~

