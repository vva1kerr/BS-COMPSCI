
# venv
* `sudo apt install python<version>-venv` # if on Debian/Ubuntu
* `python -m venv venv`
* `source venv/bin/activate`

# requirements.txt
* `pip3 install -r requirements.txt`

# streamlit
* `python3 -m streamlit run <app>.py`
* `sudo <path>/venv/bin/python -m streamlit run Home.py --server.port 80`
* `nohup python3 -m streamlit run <app>.py --server.port 80` 

# Streamlit secrets
* `streamlit secrets write secrets.toml`
#### when to use .streamlit/secrets.toml
to store api keys
* `openai_api_key = "sk-..."`
* `aws_access_key = "AKIA..."`
database credentials
* `db_username = "myuser"`
* `db_password = "mypassword"`

# streamlit config
* `streamlit config show`
