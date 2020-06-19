# Flask

## Setup

```sh
cd flask-project
virtualenv . -p python3
.\Scripts\activate
pip install flask flask-sqlalchemy
aria2c.exe "https://www.toptal.com/developers/gitignore/api/virtualenv,flask" -o .gitignore
vi app.py
python app.py
```

```py
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'index';

if __name__ == "__main__":
    app.run(debug=True)
```
