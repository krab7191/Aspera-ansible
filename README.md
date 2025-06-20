# Installing Aspera with ansible

Ansible playbooks to install Aspera HSTS, Faspex, Console, Common, and HTTP Gateway. Tested on RHEL 8.5

## Prep
1. Get Techzone reservations or other suitable servers. [This environment](https://techzone.ibm.com/collection/aspera-lab/environments) was used for these instructions.
2. Set appropriate environment variables in `env_vars.yml`
3. Download licenses to hsts.license, faspex.license, etc.
4. Get .pem files and set info in hosts files.

### Run playbooks:

#### HSTS:
`ansible-playbook -i hsts_hosts.ini aspera_hsts.yml` (Add -v / -vv / -vvv for varying levels of verbosity.)

#### Faspex:
1. `ansible-playbook -i faspex_hosts.ini aspera_faspex.yml`
2. SSH into machine and run `faspexctl setup` to finish configuration
3. Log into Faspex UI and add HSTS as managed node, default storage.
4. Set up SMTP in order to send user invite emails, etc.
5. (Optional): Add SSL certificate with certbot
   - Make sure you have a domain name (I used noip.com)
   - Fill out FASPEX_DOMAIN & WEB_ADMIN_EMAIL variables
   - Run faspex_cert.yml: `ansible-playbook -i faspex_hosts.ini faspex_cert.yml`

#### Console:
1. Run `ansible-playbook -i console_hosts.ini aspera_console.yml`
2. SSH into machine and run `asctl console:setup` to finish configuration
3. Log into Console UI and add the License and change password
4. Add HSTS node on port 33001, Default endpoint type: "Node API", and check "Create default Console groups"
5. (Optional) Set up SMTP details to enable notifications
6. (Optional) run "console_cert.yml" to install certbot certs for console: `ansible-playbook -i console_hosts.ini console_cert.yml`

#### HTTP Gateway:
1. Run `ansible-playbook -i gateway_hosts.ini aspera_gateway.yml`
2. In Faspex UI enable HTTP gateway in admin panel.
