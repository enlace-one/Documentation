
## New Application Checklist
1. Run the startapp command
```
python manage.py startapp app_name
```
2. Add to INSTALLED_APPS in settings.py
3. Add a view
4. Add a URL mapping
5. Add the URL mapping to the project in `my_project/urls.py`
Ex: `"path("app_name/", include("app_name.urls")),"`

### New Model Checklist
1. Add the model to `app_name/models.py`
2. Register it at `app_name/admin.py`

