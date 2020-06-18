# Django

## Setup

<https://www.codingforentrepreneurs.com/blog/django-on-docker-a-simple-introduction>

```sh
virtualenv . -p python3
source  bin/activate
deactivate

pip install django=3.0
pip freeze
pip freeze > requirements.txt
cd src

django-admin startproject myapp .

python .\manage.py startapp pages
python .\manage.py startapp blog

python .\manage.py makemigrations
python .\manage.py migrate

python manage.py runserver #to-run

python manage.py createsuperuser #users for admin access
```

## Template tags

<https://docs.djangoproject.com/en/3.0/ref/templates/builtins/>

```py
{% include "foo/bar.html" %}
# You can pass additional context to the template using keyword arguments:
{% include "name_snippet.html" with person="Jane" greeting="Hello" %}
# If you want to render the context only with the variables provided (or even no variables at all), use the only option. No other variables are available to the included template:
{% include "name_snippet.html" with greeting="Hi" only %}

It is {% now "jS F Y H:i" %}

# for
{% for x, y in points %}
    There is a point at {{ x }},{{ y }}
{% empty %}
    <li>Sorry, no athletes in this list.</li>
{% endfor %}

# if
{% if athlete_list %}
    Number of athletes: {{ athlete_list|length }}
{% elif athlete_in_locker_room_list %}
    Athletes should be out of the locker room soon!
{% else %}
    No athletes.
{% endif %}


{{ title|escape }} # Escapes a string’s HTML
{{ value|escapejs }}
{{ value|filesizeformat }} #Formats the value like a ‘human-readable’ file size
{{ value|first }} #Returns the first item in a list.
{{ value|json_script:"hello-data" }} #Safely outputs a Python object as JSON, wrapped in a <script> tag, ready for use with JavaScript.
{{ var|safe }} #Marks a string as not requiring further HTML escaping prior to output. When autoescaping is off, this filter has no effect. If you are chaining filters, a filter applied after safe can make the contents unsafe again. For example, the following code prints the variable as is, unescaped
{{ value|slugify }} #If value is "Joel is a slug", the output will be "joel-is-a-slug".
```

| Argument        | Outputs |
| --------------- | ------- |
| `openblock`     | `{%`    |
| `closeblock`    | `%}`    |
| `openvariable`  | `{{`    |
| `closevariable` | `}}`    |
| `openbrace`     | `{`     |
| `closebrace`    | `}`     |
| `opencomment`   | `{#`    |
| `closecomment`  | `#}`    |

| Variable              | Description                                                    |
| --------------------- | -------------------------------------------------------------- |
| `forloop.counter`     | The current iteration of the loop (1-indexed)                  |
| `forloop.counter0`    | The current iteration of the loop (0-indexed)                  |
| `forloop.revcounter`  | The number of iterations from the end of the loop (1-indexed)  |
| `forloop.revcounter0` | The number of iterations from the end of the loop (0-indexed)  |
| `forloop.first`       | True if this is the first time through the loop                |
| `forloop.last`        | True if this is the last time through the loop                 |
| `forloop.parentloop`  | For nested loops, this is the loop surrounding the current one |

## Widgets

<https://docs.djangoproject.com/en/3.0/ref/forms/widgets/>

A widget is Django’s representation of an HTML input element.

`birth_year = forms.DateField(widget=forms.SelectDateWidget(years=BIRTH_YEAR_CHOICES))`
