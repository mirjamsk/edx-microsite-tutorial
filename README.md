# Example edx microsite
This tutorial extends the [Microsites Theming overview](https://github.com/edx/edx-platform/wiki/Microsites-Theming) by providing instructions how to configure and add an example edx-microsite `foo.localhost`.

+ Edit the */etc/hosts* file on your host machine via `sudo nano /etc/hosts` by adding the following line 
```
 127.0.0.1			foo.localhost
```
+ If you are developing locally, stop all other running vagrant images of Open edX
+ Copy the *edx-microsite/* directory from this repo inside a parent directory to *edx-platform/* 
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
+ If you are developing locally, you need to add your newly created *edx-microsite/* folder to vagrant's [synced folders](https://docs.vagrantup.com/v2/synced-folders/) by modifying the `Vagranfile`. An example of a configured *Vagrantfile* is provided in this repo.
+ Edit the */edx/app/edxapp/lms.env.json* file via `sudo nano /edx/app/edxapp/lms.env.json`  by adding the following lines:
  ```
  ...
  "FEATURES": {
   ...
   "USE_MICROSITES": true
  }, 
  ...
  "MICROSITE_CONFIGURATION": {
    "foo": { 
        "domain_prefix": "foo", 
        "university": "foo", 
        "platform_name": "Foo Professional Education Online X Programs", 
        "logo_image_url":  "foo/images/header-logo.png", 
        "ENABLE_MKTG_SITE":  false, 
        "SITE_NAME": "foo.localhost", 
        "course_org_filter": "FooX", 
        "course_about_show_social_links": false, 
        "css_overrides_file":  "foo/css/style.css", 
        "show_partners":  false, 
        "show_homepage_promo_video": false, 
        "course_index_overlay_text": "Explore Foo courses from leading universities", 
        "homepage_overlay_html":  "<h1>The Footure of Online Education</h1>", 
        "favicon_path": "foo/images/header-logo.png", 
        "ENABLE_THIRD_PARTY_AUTH": false, 
        "ALLOW_AUTOMATED_SIGNUPS": true, 
        "ALWAYS_REDIRECT_HOMEPAGE_TO_DASHBOARD_FOR_AUTHENTICATED_USER": false, 
        "course_email_from_addr": "foo@edx.com", 
        "SESSION_COOKIE_DOMAIN": "foo.localhost"
    }
  }, 
  "MICROSITE_ROOT_DIR": "/edx/app/edxapp/edx-microsite", 
  ...
  ```
*An example of an entire lms.env.json file is provided in the repo.*

+ If you are developing locally:
 + restart the vagrant VM for the Vagrantfile changes to take effect: 
 + ssh back into the Vagrant `vagrant ssh `
 + start LMS: `sudo su edxapp; paver devstack lms`
 + if things are configured correctly, you should see something like this in the output console:
  ```
  [lms.startup] startup.py:127 ­ Loading microsite 
  /edx/app/edxapp/edx­microsite/foo
  ```
+ You should now be able to bring up a web browser and go to http://foo.localhost:8000
+ In order for a course to appear in the site catalog, you will need to create it in Studio with `organization` set to ‘FooX’.
