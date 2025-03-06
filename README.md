# Test Ansible Role

This is a test Ansible role that demonstrates best practices for role development and testing.

## Requirements

- Ansible 2.9 or higher
- Molecule 3.0 or higher
- Docker (for molecule testing)

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yaml
example_variable: "default_value"
example_boolean: true
example_list:
  - item1
  - item2
```

## Dependencies

None.

## Example Playbook

```yaml
---
- hosts: servers
  roles:
    - test
```

## Testing

This role uses Molecule for testing. To run the tests:

```bash
molecule test
```

The role is also tested using GitHub Actions, which runs:
- yamllint
- ansible-lint
- molecule tests

## License

MIT

## Author Information

Your Name 