Problem: Following error while apt update/upgrade
   "Encountered a section with no Package: header"

Resolution:
sudo rm /var/lib/apt/lists/* -vf
sudo apt-get update
