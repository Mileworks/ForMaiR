# [ForMaiR](https://formair.io) - auto Forward eMails with custom Rules

<p align="center">
  <a href="https://www.codefactor.io/repository/github/k8scat/formair"><img src="https://www.codefactor.io/repository/github/k8scat/formair/badge" alt="CodeFactor" /></a>
</p>

<p>
  <a href="https://github.com/k8scat/ForMaiR">GitHub</a> |
  <a href="https://gitee.com/hsowan/ForMaiR">码云</a>
</p>

## Usage

```bash
# clone repo
git clone git@github.com:k8scat/ForMaiR.git
cd ForMaiR

# copy `template/config.yaml` as your own
cp template/config.yaml config.yaml

# init python3 environment
virtualenv -p python3 .venv
source .venv/bin/activate

# install requirements
pip install -r requirements.txt

# start forwarding emails by your custom rules
python main.py config.yaml
```

## Custom rules

Emails which meet follow rules will be auto forwarded to `to_addrs`.

- [x] Email `from_addr[1]` in `from_addrs`
- [x] Email `subject` meet `subject_pattern`
- [x] Email `plain_content` or `html_content` meet `content_pattern`

```yaml
rules:
  -
    to_addrs:
      - 't1@example.com'
      - 't2@example.com'
    from_addrs:
      - 'f1@example.com'
      - 'f2@example.com'
    subject_pattern: ''
    content_pattern: ''
  -
    to_addrs:
      - 't1@example.com'
      - 't2@example.com'
    from_addrs:
      - 'f1@example.com'
      - 'f2@example.com'
    subject_pattern: ''
    content_pattern: ''
```

## Only forwarding the new emails

Support forwarding new emails in the specified range.

- Get `last_email_index` from the _index_file_ (default 0 if not exists)
- Get `email_count` from `pop3_server.stat`

```python
for index in range(last_email_index+1, email_count+1):
    pass
```
