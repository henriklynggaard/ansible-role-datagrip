DataGrip (https://www.jetbrains.com/datagrip)
=========

This role installs DataGrip and configured plugins. It has been tested on Linux Mint 18 but should work on most 
distributions. By default it installs DataGrip 2017.1.5 and no additional plugins

By default DataGrip is installed under the user's home directory and _become_ is not needed.

Requirements
------------

None


Role Variables
--------------

    datagrip_version: 2017.1.5
    datagrip_download_mirror: https://download.jetbrains.com/datagrip/
    datagrip_plugin_download_mirror: "https://plugins.jetbrains.com/plugin/download?updateId="
    datagrip_plugins: []
    datagrip_download_directory: /tmp
    datagrip_install_directory: "{{ ansible_env['HOME'] }}/Tools"

    # calculated
    datagrip_install_file: "datagrip-{{ datagrip_version }}.tar.gz"
    datagrip_download_url: "{{ datagrip_download_mirror }}{{ datagrip_install_file }}"
    datagrip_location: "{{ datagrip_install_directory }}/DataGrip-{{ datagrip_version }}"
    datagrip_desktop_file_location: "{{ ansible_env['HOME'] }}/.local/share/applications/datagrip-{{ datagrip_version }}.desktop"

datagrip_plugins is a list of names which get appended to datagrip_plugin_download_mirror to form a full download  


Dependencies
------------

None

Example 
-------

__Example playbook__


    - hosts: localhost
      connection: local
    
    roles:
      - henriklyngaard.datagrip
      
__Exmaple inventory for plugins__

The below IDs have been found by going to https://plugins.jetbrains.com/dbe and searching for the plugin. 
Once found copy the link location for the desired version and use the _updateId=XXXXX_ part at the end        
      
    datagrip_plugins:
      # ignore 1.7.6
      - 32828
      # bash support 1.6.5.171
      - 31610
      # ansible 0.9.4
      - 27616
      # docker 2.5.3
      - 33621
      # markdown 2017.1.20170302
      - 33092      
      
 Alternatively upload the required plugins to a webserver and adjust _datagrip_plugin_download_mirror_ and 
 _datagrip_plugins_ accordingly
      
      
License
-------

MIT

Change log
----------

* 1.0: Initial version
