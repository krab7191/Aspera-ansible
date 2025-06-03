# Installing Aspera with ansible

## Prep
1. Set appropriate environment variables in `env_vars.yml`
2. Download licenses to hsts.license, faspex.license, etc.
3. Get .pem files and set info in hosts.ini

### Run playbooks:

#### HSTS:
`ansible-playbook -i hosts.ini aspera_hsts.yml` (Add -v / -vv / -vvv for varying levels of verbosity.)
