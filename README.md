# Django in Teamwork - Writen by Khoa Huynh
## Django, Python Convention
### PEP 8
- PEP 8 is the official style guide for Python. We advise reading it in detail and learn to follow the PEP 8 coding conventions: (PEP8)[python.org/dev/peps/pep-0008/]
- PEP 8 describes coding conventions such as:
  - Use 4 spaces per indentation level.
  - Separate top-level function and class definitions with two blank lines.
  - Method definitions inside a class are separated by a single blank line.
### The 79-Character Limit in line
```
# Bad Example
print('Hello, Im Khoa and this is 79 characterrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrr end of 79 character')
# Do thing
print('Hello, Im Khoa and this is 79 characterrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrrr'
    ' end of 79 character'
)
```
### The word on imports
- PEP 8 suggests that imports should be grouped in the following order:
  - Standard library imports.
  - Imports from core Django.
  - Imports from third-party apps including those unrelated to Django.
  - Imports from the apps that you created as part of your Django project
- When we’re working on a Django project, our imports look something like the following:
    ```
    # Stdlib imports
    from math import sqrt

    from os.path import abspath


    # Core Django imports
    from django.db import models

    from django.utils.translation import ugettext_lazy as _


    # Third-party app imports
    from django_extensions.db.models import TimeStampedModel


    # Imports from your apps
    from splits.models import BananaSplit
    ```
### Use Explicit Relative Imports
- When writing code, it’s important to do so in such a way that it’s easier to move, rename, and version
your work
    ```
    # Bad Example
    from student.models import Student

    from student.forms import StudentForm

    from core.views import StudentViews
    ```
    - Sure, your Studnet app works fine within your project, but it has those nasty implicit relative imports that make it less portable and reusable

- Convert to good

```
    # Good Example
    from .models import Student

    from .forms import StudentForm

    from core.views import StudentViews
```
- Compare Import types in Django

|  Code |  Import Type  | Usage  | 
|---    |---|---|
|`from core.views import StudentView`|absolute import|Use when importing from outside the current app |
|`from .models import Student`|explicit relative|Use when importing from another module in the current app  |
|`from models import Student`|implicit relative|Often used when importing from another module in the current app, but not a good idea  |
### Avoid using import *
- Take whatever you need
    ```
    # Do thing
    from django import forms

    from django.db import models

    # Don't do this
    from django.forms import *

    from django.db.models import *
    ```
- The reason for this is to avoid implicitly loading all of another Python module’s locals into and over our current module’s namespace, this can produce unpredictable and sometimes catastrophic results
- Sometimes we will encounter the case of having the same Name in Django modules

    ```
    from django.db.models import CharField

    from django.forms import CharField
    ```
    -  Try this for solve problem

    ```
    from django.db.models import CharField as ModelCharField

    from django.db.forms import CharField as FormCharField
    ```
### Django Coding Style
- Please read it (here)[https://docs.djangoproject.com/en/3.2/internals/contributing/writing-code/coding-style/]
### Use Underscores in URL Pattern Names Rather Than Dashes 
    ```
    # Bad Example
    patterns = [
        url(regex='^add/$', view=views.add_topping, name='add-topping'),
    ]

    # Do this
    patterns = [
        url(regex='^add/$', view=views.add_topping, name='add_topping'),
    ]

    # I recommend changing all name in urls is same. but not use Underscores in path
    patterns = [
        url(regex='^add-topping/$', view=views.add_topping, name='add_topping'),
    ]
    ```
### Tips and Tool for help 
- Pre-commit checks
  - pre-commit is a framework for managing pre-commit hooks. These hooks help to identify simple issues before committing code for review. By checking for these issues before code review it allows the reviewer to focus on the change itself, and it can also help to reduce the number CI runs.
- To use the tool, first install pre-commit and then the git hooks:

    ```
    $ python -m pip install pre-commit
    $ pre-commit install
    ```
