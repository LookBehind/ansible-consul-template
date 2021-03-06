consul-template
==============

Ansible role to install, configure and run consul-template as a service.

> **Breaking Changes**:
>    * Latest version of this role now ONLY supports consul-template v0.18+.
>    * Please use c841ac8641b309b83073d462a42cb3234d1772ab, for support of 
>      consul-template v0.16 and earlier.


## Example

### Install and start consul-template as a service, and ADD template configurations

> **NOTE:**
>    This role expects that ctmpl file to render for a given template config
>    (i.e. value of `consul_template_template.source`) already exist.
>    You **MUST** ensure it exists on the remote host before adding the template
>    configuration. This is because consul-template will error on restart if missing

```
- hosts: myhost

  vars:
    consul_template_version: 0.18.5
    consul_template_consul_address: "<consulhost:consulport>"
    
  roles:
    - role: wunzeco.consul-template
      consul_template_template:
        source: "/data/nginx/templates/jenkins-8080-include.conf.ctmpl"
        destination: "/data/nginx/includes/common/jenkins-8080.conf"

    - role: wunzeco.consul-template
      consul_template_template:
        source: "/data/nginx/templates/jenkins-8080-upstream.conf.ctmpl"
        destination: "/data/nginx/upstream/jenkins-8080.conf"
```


## Testing

To run this role's integration tests

```
kitchen test
```


## Dependencies

none

## Outstanding
- redirect consul-template logs to file for service started by systemd
