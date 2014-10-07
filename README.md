# prepare-release

Prepare-release checks out the next application version from your GIT scm, symlinks common folders and files and creates necessary folders etc.

Forms a traditional deployment cycle in conjunction with [rails-deployment][1] and [finalize-release][2].

example usage:

    ---
    - hosts: server
      user: app
      gather_facts: False
      vars:
        user: app
        home_directory: "/home/{{ user }}"
        deploy_to: "{{ home_directory }}"

      roles:
        -
          role: nicolai86.prepare-release

          repo: git@example.com:app
          branch: develop

          symlinks:
            - { src: "{{ shared_path }}/vendor/bundle", dest: "{{ build_path }}/vendor/bundle" }
            - { src: "{{ shared_path }}/public/assets", dest: "{{ build_path }}/public/assets" }
            - { src: "{{ shared_path }}/log", dest: "{{ build_path }}/log" }
            - { src: "{{ shared_path }}/.env", dest: "{{ build_path }}/.env" }
            - { src: "{{ shared_path }}/config/database.yml", dest: "{{ build_path }}/config/database.yml" }

          directories:
            - "{{ shared_path }}/config"

          templates:
            - { src: "templates/env.js", dest: "{{ shared_path }}/.env" }


prepare a new release of any GIT versioned software using ansible

[1]:https://github.com/nicolai86/ansible-rails-deployment
[2]:https://github.com/nicolai86/ansible-finalize-release
