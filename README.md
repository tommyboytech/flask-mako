Flask Mako Templates
====================

Provides support for Mako Templates in Flask. Based on code from flask-mako,
flask-genshi and flask itself.

currently:

    from flask import Flask
    from flask_mako import MakoTemplates, render_template

    app = Flask(__name__)
    mako = MakoTemplates(app)
   
    @app.route('/')
    def index():
       return "Hello World !"
       
       
Documentation: http://packages.python.org/Flask-Mako/

PyPI: http://pypi.python.org/pypi/Flask-Mako/


### todo 

- testing
- document a little better
