# Overview
A framework for writing small, readable tests for Python programs

### Use
Code:
```python
# content of test_sample.py
def func(x):
    return x + 1

def test_answer():
    assert func(3) == 5
```
Command:
```bash
pytest
```
### Installation
```bash
pip install pytest
```
# Best Practices
### Project Structure
Pytest will run all files of the form test_x.py or x_test.py  in the current directory or subdirectories
- run tests in a module: `pytest <module name>.py`
- run tests in a directory: `pytest <directory name>`
- get slowest 10 test durations over 1.0s interval: `pytest --durations=10 --durations-min=1.0`
- `-x` flag will stop testing after the first failure
- `--maxfail=2` flag will stop testing after the second failure
- `--pdb` flag initiates debugger after failure
# Technical
### Fixtures
Pass arguments to pytest function for setup
```python
# content of test_emaillib.py
from emaillib import Email, MailAdminClient

import pytest

@pytest.fixture
def mail_admin():
    return MailAdminClient()

@pytest.fixture
def sending_user(mail_admin):
    user = mail_admin.create_user()
    yield user
    mail_admin.delete_user(user)

@pytest.fixture
def receiving_user(mail_admin, request):
    user = mail_admin.create_user()

    def delete_user():
        mail_admin.delete_user(user)

    request.addfinalizer(delete_user)
    return user

@pytest.fixture
def email(sending_user, receiving_user, request):
    _email = Email(subject="Hey!", body="How's it going?")
    sending_user.send_email(_email, receiving_user)

    def empty_mailbox():
        receiving_user.clear_mailbox()

    request.addfinalizer(empty_mailbox)
    return _email

def test_email_received(receiving_user, email):
    assert email in receiving_user.inbox
```