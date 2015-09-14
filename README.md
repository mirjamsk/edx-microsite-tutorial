# title Edx
This tutorial extends the [Microsites Theming overview](https://github.com/edx/edx-platform/wiki/Microsites-Theming) by providing instructions how to configure and add an example edx-microsite `foo.localhost`.

+ Edit the `/etc/hosts` file on your host machine by adding the following line 
```
 127.0.0.1			foo.localhost
```
+ If you are developing locally, stop all other running vagrant images of Open edX
+ Copy the *edx-microsite/* directory from this repo inside a parent directory to *edx-platform*. 
 + This should leave your folder structure looking like this:
```
- /
  - edx-platform/
  - edx-microsite/
    - foo/
      - css/
      - images/
      - templates/
  ...
```
+ If you are developing locally, you need to add your newly created *edx-microsite/* folder to vagrant's [synced folders](https://docs.vagrantup.com/v2/synced-folders/) by modifying the *Vagranfile*. An example of a configured *Vagrantfile* is provided in this repo
+ Modify the *lms.envs.json* file by adding the following lines
