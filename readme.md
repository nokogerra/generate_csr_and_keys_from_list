## Generate openssl configs, CSRs and keys from a list of FQDNs (SANs)
This simple role is intended to run on a localhost, so you don't need an inventory file.<br />
It creates a directory structure for openssl configs (from the openssl.conf.j2), CSRs and keys:<br />
- /home/ansible_user_id/csrs_and_keys/configs
- /home/ansible_user_id/csrs_and_keys/reqs
- keys
and then creates openssl configs, reqs and keys based on "common_names" variable (list). It is assumed you gonna have a single SAN per certificate, so if you need multiple SANs, then the variable should look different and template must have a loop (prob, will do it later).<br />
Check all the variables in defaults/main.yml.