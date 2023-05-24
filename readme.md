## Generate openssl configs, CSRs and keys from a list of FQDNs (SANs)
This simple role is intended to run on a localhost, so you don't need an inventory file, but you need an installed openssl.<br />
It creates a directory structure for openssl configs, CSRs and keys:<br />
- /home/ansible_user_id/csrs_and_keys/configs
- /home/ansible_user_id/csrs_and_keys/reqs
- /home/ansible_user_id/csrs_and_keys/keys<br />
After that the role creates an openssl config for each item in a list. Here is an example of the list:
```
    common_names:
      - cn: "vasyan.nokogerra.lab"
      - cn: "*.wildcard.com"
      - cn: "taras.nokogerra.lab"
        sans:
          - "DNS.1 = taras.nokogerra.lab"
          - "DNS.2 = one.taras.nokogerra.lab"
          - "DNS.3 = one.taras.nokogerra.lab"
          - "IP.1 = 1.1.1.1"
          - "IP.2 = 2.2.2.2"
```
- In case of "vasyan.nokogerra.lab", it's gonna be used not only as a Common Name, but also as a SAN;
- In case of "*.wildcard.com" - the same, but for a wildcard Name and SAN;
- In case of "taras.nokogerra.lab", the name is used as a Common Name, and all the items in "sans" are used as SANs (**don't forget about "DNS.x and IP.x phrases"**).<br />
For the complete list of variables see **defaults/main.yml**.<br />
You can check your CSRs and keys like that:
```
openssl req -in $HOME/csrs_and_keys/reqs/taras.nokogerra.lab.csr -text -noout
openssl rsa -in $HOME/csrs_and_keys/keys/taras.nokogerra.lab.key -text -noout
```
