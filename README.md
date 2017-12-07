
### Infrastructure

AWS EC2 instances and Route53 for domain management, this was done initially manually but see `provision_aws_infra` for a working example of adding this piece as well.




### Servers

 * [Github JPetStore](https://github.com/Perficient-DevOps/jpetstore-6)
 * [Jenkins OSS](http://jenkins.devopsinabox.perficientdevops.com:8080)
 * [Nexus OSS](http://nexus.devopsinabox.perficientdevops.com:8081)
 * JPetStore [Dev](http://tomcat.devopsinabox.perficientdevops.com:8081/JPetStore) / [QA](http://tomcat.devopsinabox.perficientdevops.com:8082/JPetStore) / [UAT](http://tomcat.devopsinabox.perficientdevops.com:8083/JPetStore) / [PROD](http://tomcat.devopsinabox.perficientdevops.com:8084/JPetStore)
 * [UCD](https://deploy.devopsinabox.perficientdevops.com/)
 * [UCR](https://release.devopsinabox.perficientdevops.com/)

### Software installations

Setup ansible dependencies


    ansible-galaxy install -r requirements.yml

### Working with passwords

You need to create you local vault password file. I have hard-coded this into the `ansible.cfg` for this project to be `~/.ansible/etc/aws-doiab` so once you get the super secret password, create this file and all the commands below will work.


Testing:

This is example is for a group variable to be stored in `group_vars\jenkins.yml`

    $ ansible-vault encrypt_string --name jenkins_admin_password 's3cr3t'
    jenkins_admin_password: !vault |
              $ANSIBLE_VAULT;1.1;AES256
              35653038386461633032653338613062623633396563373537326461643131323139383132376138
              6534616634323333303261313239356338363164393734380a306433646637613662613233343636
              33306436376232626235353462623763306336626466623064363762336665666134363366663237
              3765333633656633610a636665316565643130356365393738376664366639336537323537303531
              6564
    Encryption successful

Now add this value to the file `group_vars\jenkins.yml`, and we can run a test to see against that same group.

    $ ansible jenkins -m debug -a 'var=jenkins_admin_password'
    jenkins.devopsinabox.perficientdevops.com | SUCCESS => {
        "jenkins_admin_password": "s3cr3t"
    }


### Demo Scenarios

Build from GitHub project using Pipeline.
