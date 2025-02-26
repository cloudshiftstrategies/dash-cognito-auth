# Dash Cognito Auth

Dash Cognito Auth is a simple library using Cognito OAuth to authenticate and
view a [Dash](https://dash.plot.ly/) app.

This Library uses [Flask Dance](https://github.com/singingwolfboy/flask-dance)
and a modified version of Plotly's own [dash auth](https://github.com/plotly/dash-auth)
for authentication.

This Library is heavily inspired by [dash-google-oauth](https://github.com/lchapo/dash-google-auth) created by Lucas Chapin

## Basic Use

Authentication can be added to your Dash application using the `CognitoOAuth`
class, i.e.

```python
from dash import Dash
from flask import Flask
from dash_cognito_auth import CognitoOAuth

server = Flask(__name__)
server.config.update({
  'COGNITO_OAUTH_CLIENT_ID': ...,
  'COGNITO_OAUTH_CLIENT_SECRET': ...,
})

app = Dash(__name__, server=server, url_base_pathname='/')

additional_scopes = [...]
auth = CognitoOAuth(app, domain='mydomain', region='eu-west-1', authorized_emails, additional_scopes)

# your Dash app here :)
...
```

## Example
Steps to try this out yourself:

1. Install the `dash-cognito-auth` library using `pip`:

    ```bash
    $ pip install dash-cognito-auth
    ```

2. Follow the [Flask Dance Guide](http://flask-dance.readthedocs.io/en/latest/quickstarts/cognito.html)
   to create an app on the cognito admin console

3. Make a copy of [app.py](https://github.com/lucaschapin/dash-cognito-auth/blob/master/app.py)
   and set the variables (or set the corresponding environment variables):
    ```python
    server.config["COGNITO_OAUTH_CLIENT_ID"] = ...
    server.config["COGNITO_OAUTH_CLIENT_SECRET"] = ...
    ```
   with values from the Cognito OAuth 2 client you should have set up in step 1.
   If you've set these up properly, you can find them at
   [APIs & Services > Credentials](https://console.developers.cognito.com/apis/credentials)
   under the section **OAuth 2.0 client IDs**.

4. Run `python app.py` and open [localhost](http://localhost:8050/) in a
   browser window to try it out! If the app loads automatically without
   prompting a Cognito login, that means you're already authenticated -- try
   using an incognito window in this case if you want to see the login
   experience for a new user.
