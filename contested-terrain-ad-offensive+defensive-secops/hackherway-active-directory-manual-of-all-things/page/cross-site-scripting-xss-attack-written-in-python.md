# Cross Site Scripting (XSS) Attack Written in Python

Cross-Site Scripting (XSS) Attack Written in Python

Cross-Site Scripting (XSS)

XSS is an attack that injects malicious scripts into content from otherwise trusted websites.

from flask import Flask, request

app = Flask(\_\_name\_\_)

@app.route("/")

def xss\_example():

user\_input = request.args.get('input')

\# Vulnerable to XSS

return f"\<html>\<body>Search results for: {user\_input}\</body>\</html>"

if \_\_name\_\_ == "\_\_main\_\_":

app.run(debug=True)

**How to Test**

* Run the Flask app, then visit: http://127.0.0.1:5000/?input=\<script>alert(‘XSS’)\</script>
