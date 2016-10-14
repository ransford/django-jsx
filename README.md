# django-jsx

Django-JSX is a integration tool for Django projects using the excellent React
UI library. It enables direct embedding of the JSX syntax into Django templates
through a `{% jsx %}` template block. Your JSX will be extracted and compiled
along with your other front-end assets and rendered into your page.

Django-JSX makes React and Django work together.

## Features

- Embed React's JSX syntax directly into your project's Django templates
- Access the template's context variables inside your JSX attribute expressions
- Expose your library of React components to your traditional template developers


## Installation and Use

django-jsx requires Django >= 1.8 and Python >= 2.7 or >= 3.3.

To install from PyPi:

    pip install django-jsx

Add django-jsx to your Django settings' `INSTALLED_APPS`:

    INSTALLED_APPS = [
        ...
        'django_jsx',
    ]

Now, in your templates, you can use JSX and React components within a `{% jsx %}`
block easily.

    {% load jsx %}
    {% jsx %}
        <Dropdown input="section" options={sectionOptions} />
    {% endjsx %}

You'll need to include Django-JSX into your front-end build process. This includes
two steps. First, you need to run the `compilejsx` management command, which will
generate your "JSX Registry". This creates an ES6/JSX module you'll place with your
other front-end assets.

    python manage.py compilejsx -o project/static/js/jsx_registry.js

Now that all the inline JSX you used in your templates is extracted for your
front-end to use, you'll import those JSX snippets and render them all. You are
responsible for making all your React components available for this step in
the process.

    import jsxRegistry from './jsx_registry.js'
    import DropdownWidget from './widgets/dropdown.js'
    import LoadingWidget from './widgets/loading.js'

    jsxRegistry.renderAllDjangoJSX({
        DropdownWidget,
        LoadingWidget
    })



## License

django-jsx is released under the BSD License. See the
[LICENSE](https://github.com/caktus/django-jsx/blob/master/LICENSE) file for more details.


### Contributing

If you think you've found a bug or are interested in contributing to this project
check out [django-jsx on Github](https://github.com/caktus/django-jsx).

Development sponsored by [Caktus Consulting Group, LLC](http://www.caktusgroup.com/services).