# Use cloudinary within wagtail

## About
This package adds Cloudinary support to Wagtail CMS.

So far you can browse the images in cloudinary and add upload to cloudinary ONLY in the image chooser within a page.

## To do (maybe)
- modeladmin for cloudinary images
- maybe remove wagtailimages from the admin menu or at least make it clear they are separate things.

## Installation
To install the package you can use the master branch like this:
```
pip install -e git+git://github.com/emg36/wagtailcloudinary.git#egg=wagtailcloudinary
```
Or you can used a stable version:
```
pip install -e git+git://github.com/emg36/wagtailcloudinary.git@v0.3.1#egg=wagtailcloudinary
```

## Configuration
Add app wagtailcloudinary in your INSTALLED_APPS list

```
INSTALLED_APPS = [
    ...
    'wagtailcloudinary',
    ...
]
```

in settings.py put your cloud_name, api_key and apy_secret into cloudinary configuration

```
import cloudinary

cloudinary.config(
    cloud_name=<YOUR_CLOUDINARY_CLOUD_NAME>,
    api_key=<YOUR_CLOUDINARY_API_KEY>,
    api_secret=<YOUR_CLOUDINARY_API_SECRET>,
)
```

## Usage

in models.py

```
from wagtail.admin.edit_handlers import FieldPanel
from wagtail.core.models import Page
from wagtailcloudinary.fields import CloudinaryField, CloudinaryWidget

class SomePage(Page):
    image = CloudinaryField()

    content_panels = Page.content_panels + [
        FieldPanel('image', widget=CloudinaryWidget),
    ]
```

in urls.py

```
...

from wagtailcloudinary import site as cloud_site

urlpatterns = [
    ...
    url(r'^cloundinary_images/', cloud_site.urls),
    ...
    url(r'', include(wagtail_urls)),
]
```
