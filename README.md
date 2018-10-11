[![Build Status](https://travis-ci.org/open-io/ansible-role-openio-oio-blob-rebuilder.svg?branch=master)](https://travis-ci.org/open-io/ansible-role-openio-oio-blob-rebuilder)
# Ansible role `blob_rebuilder`

An Ansible role for the blob rebuilder. Specifically, the responsibilities of this role are to:

- Install
- Configure

## Requirements

- Ansible 2.4+

## Role Variables


| Variable   | Default | Comments (type)  |
| :---       | :---    | :---             |
| `openio_blob_rebuilder_allow_same_raw` | `false` | ... |
| `openio_blob_rebuilder_chunks_per_second` | `30` | ... |
| `openio_blob_rebuilder_event_agent_url` | `"beanstalk://{{ ansible_default_ipv4.address }}:6014"` | ... |
| `openio_blob_rebuilder_gridinit_dir` | `"/etc/gridinit.d/{{ openio_blob_rebuilder_namespace }}"` | ... |
| `openio_blob_rebuilder_gridinit_file_prefix` | `""` | ... |
| `openio_blob_rebuilder_gridinit_on_die` | `respawn` | ... |
| `openio_blob_rebuilder_gridinit_start_at_boot` | `true` | ... |
| `openio_blob_rebuilder_namespace` | `"OPENIO"` | ... |
| `openio_blob_rebuilder_provision_only` | `false` | ... |
| `openio_blob_rebuilder_serviceid` | `"0"` | ... |
| `openio_blob_rebuilder_worker` | `10` | ... |

## Dependencies
No dependencies.

## Example Playbook

```yaml
- hosts: all
  gather_facts: true
  become: true
  vars:
    NS: OPENIO
  roles:
    - role: repo
      openio_repository_no_log: false
      openio_repository_products:
        sds:
          release: "18.04"
    - role: namespace
      openio_namespace_name: "{{ NS }}"
    - role: gridinit
      openio_gridinit_namespace: "{{ NS }}"
      openio_gridinit_per_ns: true
    - role: blob_rebuilder
      openio_blob_rebuilder_namespace: "{{ NS }}"
      #openio_blob_rebuilder_allow_same_raw: true
      openio_blob_rebuilder_worker: 1
      openio_blob_rebuilder_chunks_per_second : 1
```


```ini
[all]
node1 ansible_host=192.168.1.173
```

## Contributing

Issues, feature requests, ideas are appreciated and can be posted in the Issues section.

Pull requests are also very welcome.
The best way to submit a PR is by first creating a fork of this Github project, then creating a topic branch for the suggested change and pushing that branch to your own fork.
Github can then easily create a PR based on that branch.

## License

Apache License, Version 2.0

## Contributors

- [Cedric DELGEHIER](https://github.com/cdelgehier) (maintainer)
