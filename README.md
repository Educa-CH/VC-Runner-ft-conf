# Python Flask App Documentation

## Introduction
This documentation will guide you through the process of understanding and running a Python Flask app. The app utilizes Flask to create a simple web page that connects to external APIs and uses them to perform various functions. The app also utilizes qrcode and requests libraries to generate QR codes and send requests to external APIs.

## Setup and Installation
To run this app, you need to have Python 3 installed on your computer. You can download Python 3 from the official Python website: https://www.python.org/downloads/. Make sure pip is installed.

Create a virtual environment with: 

```
python3 -m venv env

```
and activate it with:

```
source env/bin/activate
```

Once you have installed Python 3, you need to install the required packages in the virtual environement by running the following command in your terminal or command prompt:

```
pip install -r requirements.txt
```

After installing the required packages, you can run the app by running the following command in your terminal or command prompt: 

```
python app.py
```

This will start the Flask development server and make the app available at http://localhost:5000/. You can then access the app by navigating to that URL in your web browser.

## App Functionality
The app has four main routes:

/ - This is the root route that generates a QR code and displays it on the home page. The QR code is generated using the qrcode library and contains a URL that is retrieved from an external API using the requests library.

/check_connection/ - This route checks the connection status of an external API by making a GET request to the API endpoint. The connection status is determined by checking the response text of the request.

/name - This route is used to submit a name to an external API. When the user submits their name, the app sends a POST request to an external API using the requests library. The external API uses the name to generate a credential for the user and returns a process ID that is stored in the app's session.

/loading/ - This route checks the acceptance status of the credential by making a GET request to the external API. The acceptance status is determined by checking the response text of the request.

/success - This route is displayed after the user has successfully submitted their name and the external API has accepted the credential.

## Security
This application includes several security measures:

Cross-Origin Resource Sharing (CORS) is enabled using the CORS extension for Flask.
The Talisman extension is used to set a default content security policy for the app, allowing resources to be loaded from the same origin, any origin, or unsafe inline content.
The SESSION_COOKIE_SAMESITE attribute is set to "None", allowing session cookies to be sent with cross-site requests.
The SESSION_COOKIE_SECURE attribute is set to True, ensuring that session cookies are only sent over secure connections.
User sessions are managed using the Flask-Session extension, which stores session data on the file system and performs cleanup when the number of files reaches a certain threshold.

## Setting up Gunicorn
Run the Flask application using Gunicorn:

Make sure to replace register-ft.educa.ch with your own domain name in `gunicorn.conf.py`, and the paths to the SSL certificate files with the correct paths for your own system.

To start the Gunicorn server, run the following command in your terminal:

```
gunicorn app:app -c gunicorn.conf.py &
```
This will start the server with the specified configuration, and run it in the background (& at the end of the command). You should see output similar to the following:

```
[2023-04-17 12:34:56 +0000] [1234] [INFO] Starting gunicorn 20.1.0
[2023-04-17 12:34:56 +0000] [1234] [INFO] Listening at: https://register-ft.educa.ch:443 (1234)
[2023-04-17 12:34:56 +0000] [1234] [INFO] Using worker: gthread
[2023-04-17 12:34:56 +0000] [1237] [INFO] Booting worker with pid: 1237
[2023-04-17 12:34:56 +0000] [1238] [INFO] Booting worker with pid: 1238
You can now access the web application by visiting https://register-ft.educa.ch in your web browser.
```

## Files
The app consists of a single Python file, app.py, which contains all the routes and logic for the app. The file is organized into four main sections, each containing the logic for one of the app's routes.

## Conclusion
Congratulations! You have successfully learned how to build and run a Flask app that utilizes external APIs and libraries to perform various functions. Feel free to modify the app and experiment with new features!
