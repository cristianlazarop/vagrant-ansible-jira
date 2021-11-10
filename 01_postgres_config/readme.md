# Postgres Config



- If you want to skip the install of Postgres, then you need to run with `--extra-vars "options=install"`. Tags are crap. They are either explicit whitelists or explicit blacklist, but do not allow the logic for "explicit opt-in for an action". See [docs](https://docs.ansible.com/ansible/latest/user_guide/playbooks_tags.html#selecting-or-skipping-tags-when-you-run-a-playbook).







```
ansible-playbook \
--inventory ubuntu@192.168.178.33, \
--extra-vars "ansible_ssh_pass=123" \
--ask-become-pass \
--verbose \
--extra-vars "include=install" \
playbook.yml
```

