# Building Django apps: why are we using REST framework?

### An example
Before delving into REST framework, let's first look at a code snippet that I have written without using REST.

views
```
class EventCreateView(FormView):
    template_name = 'calendars/event.html'
    form_class = EventForm
  
    
    def dispatch(self, request, *args, **kwargs):
        if not request.user.is_authenticated:
            return HttpResponse('UNAUTHORIZED', status=401) 
        try:
            self.calendar = Calendar.objects.get(id=self.kwargs.get('calendar_id'))
        except Calendar.DoesNotExist:
            return HttpResponse('NOT FOUND', status=404)
        if self.calendar.owner != request.user:
            return HttpResponse('FORBIDDEN', status=403)
        return super().dispatch(request, *args, **kwargs)
 
    def form_valid(self, form):
        event = form.save(commit=False)
        event.calendar = self.calendar
        event.save()
        return HttpResponseRedirect(reverse('calendars:event_details', kwargs={'event_id': event.id}))
 
    def form_invalid(self, form):
        return super().form_invalid(form) 
 
    def get_form_kwargs(self):
        kwargs = super().get_form_kwargs()
        kwargs['calendar_id'] = self.kwargs.get('calendar_id')
        return kwargs
```
models
```
class Event(models.Model):
    name = models.CharField(max_length=50)
    description = models.TextField(max_length=200, blank=True)
    date = models.DateField()
    start_time = models.TimeField()
    duration = models.IntegerField(default=30)
    last_modified = models.DateTimeField(auto_now=True)
    calendar = models.ForeignKey(Calendar, on_delete=models.CASCADE, related_name='events')

```
forms
```
class EventForm(forms.ModelForm):
    class Meta:
        model = Event
        fields = ['name', 'description', 'date', 'start_time', 'duration']
        widgets = {
            'date': forms.DateInput(format=('%Y-%m-%d'), attrs={'type': 'date'}),
            'start_time': forms.TimeInput(format=('%H:%M'), attrs={'type': 'time'}),
        }
        error_messages = {
            'name': {'required': "This field is required"},
            'date': {
                'required': "This field is required",
                'invalid': "Enter a valid date (YYYY-MM-DD)"
            },
            'start_time': {
                'required': "This field is required",
                'invalid': "Enter a valid time (hh:mm)"
            },
            'duration': {'required': "This field is required"},
        }
    def __init__(self, *args, **kwargs):
        self.calendar_id = kwargs.pop('calendar_id', None)
        super().__init__(*args, **kwargs)
```
Again, let us take another look when using REST framework to build similar functionalities.
views
```
from rest_framework import viewsets
from rest_framework.permissions import IsAuthenticated
from .models import Event
from .serializers import EventSerializer

class EventViewSet(viewsets.ModelViewSet):
    queryset = Event.objects.all()
    serializer_class = EventSerializer
    permission_classes = [IsAuthenticated]

    def get_queryset(self):
        return self.queryset.filter(calendar_id=self.kwargs['calendar_id'])

    def perform_create(self, serializer):
        serializer.save(calendar_id=self.kwargs['calendar_id'])
```
models
```
from django.db import models

class Event(models.Model):
    name = models.CharField(max_length=50)
    description = models.TextField(max_length=200, blank=True)
    date = models.DateField()
    start_time = models.TimeField()
    duration = models.IntegerField(default=30)
    calendar = models.ForeignKey('Calendar', on_delete=models.CASCADE, related_name='events')
```
serializers
```
from rest_framework import serializers
from .models import Event

class EventSerializer(serializers.ModelSerializer):
    class Meta:
        model = Event
        fields = ['id', 'name', 'description', 'date', 'start_time', 'duration', 'calendar']
```
what are the differences?
we can clear see that in order to achieve similar results, Rest frameworks seems to achieve this with less code, but what are other differences that we deem important.

In general, here are the things that REST does better:

1.Client-Server Decoupling: DRF enables a clean separation of concerns, allowing frontend developers to work independently of the backend by adhering to the API contract, whereas the traditional forms way add more dependency on frontend from backend.

2.Cross-Platform Compatibility: DRF provides a JSON API out of the box, which can be consumed by any client capable of making HTTP requests, regardless of the programming language or platform. 

3.Authentication Flexibility: DRF supports various authentication mechanisms out of the box, including token authentication, which is ideal for mobile apps and SPA (Single Page Application) web clients.

### Genral comparisons
Here are some pros and cons for REST vs traditional views and form way of writing in Django.

Traditional Django

Pros:
Tight Integration with Django's Template System: Traditional Django development is closely integrated with its template system, making it straightforward to render server-side HTML based on context data.
Rapid Development for Web Pages: For applications that primarily serve HTML content, traditional Django allows for quick development cycles, especially with features like the admin interface and generic views.
Form Handling and Validation: Django forms provide a robust system for handling form submissions, including validation and error handling, without requiring additional packages.

Cons:
Limited to Server-Side Rendering: This approach is mainly suitable for applications that deliver content in HTML format, rendered server-side. It might not be as flexible for modern, dynamic web applications that require asynchronous data fetching and manipulation.
Less Suitable for API Development: While Django can serve JSON responses through views, building complex APIs without a framework like DRF can be cumbersome, requiring manual handling of serialization, request parsing, and more.

Django REST Framework (DRF)

Pros:
Designed for API Development: DRF is specifically designed to build web APIs, offering comprehensive support for serialization, request parsing, and formatting responses in various content types (JSON, XML, etc.).
Built-in Authentication and Permissions: DRF includes a flexible authentication and permissions system, supporting a wide range of methods (Token, OAuth, SessionAuthentication, etc.) out-of-the-box.
Browsable API: DRF's browsable API is a powerful feature for development and testing, allowing developers and clients to interact with the API directly through a web browser.
Client-Server Decoupling: Favorable for modern web applications, especially Single Page Applications (SPAs) and mobile apps, where the frontend and backend operate independently.
Automatic URL Routing: DRF provides router classes that automatically generate URL patterns for API views, simplifying the process of creating and maintaining URLs for large APIs.

Cons:
Steeper Learning Curve: Learning DRF requires understanding RESTful principles and additional concepts on top of Django's core features.
Overhead for Simple Applications: For simple applications or when only a few API endpoints are needed, DRF might introduce unnecessary complexity and overhead.
More Setup Required for Simple Actions: Actions like serving a simple form submission and rendering a response can be more straightforward with traditional Django views and forms than setting up a DRF serializer and viewset.

So in general, When building server-rendered web applications that do not require a decoupled frontend, or when developing applications that primarily serve HTML content, we use the traditional way of Django, but for building APIs, especially when you need to serve multiple clients (web, mobile, third-party integrations), require complex data handling, or prefer to decouple your frontend from your backend, REST framework is bettter idea.