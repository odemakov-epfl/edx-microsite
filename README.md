# sms-microsite

- Create working directory, checkout this repo and edx-microsite

```
mkdir ~/some-folder
cd ~/some-folder
git checkout https://github.com/odemakov-epfl/sms-microsite.git
git checkout ssh://git@c4science.ch/source/edx-microsite.git
```

- Edit the /etc/hosts file on your host machine, add

```
127.0.0.1       edx-test.phzh.ch.localhost
```

- Init and start VMs

```
cd sms-microsite
vagrant up
```

- Login to VM

```
vagrant ssh
sudo su edxapp
```

- Add admin user

```
/edx/bin/python.edxapp /edx/app/edxapp/edx-platform/manage.py lms --settings=devstack createsuperuser --username admin
```

- Edit file /edx/app/edxapp/lms.env.json

```
"FEATURES": {
    "USE_MICROSITES": true
```

```
    "MICROSITE_CONFIGURATION": {
        "edx-test.phzh.ch": {
            "domain_prefix": "edx-test.phzh.ch",
            "university": "PHZH",
            "platform_name": "PHZH Moocs",
            "logo_image_url": "edx-test.phzh.ch/images/logo.jpg",
            "ENABLE_MKTG_SITE": false,
            "SITE_NAME": "edx-test.phzh.ch.localhost:8000",
            "course_org_filter": "PHZH",
            "course_about_show_social_links": false,
            "show_partners": false,
            "show_homepage_promo_video": false,
            "course_index_overlay_text": "Explore free courses for edx-test.phzh.ch.",
            "homepage_overlay_html": "<h1>PHZH Moocs</h1><h2>For anyone, anywhere, anytime and here</h2>",
            "ENABLE_THIRD_PARTY_AUTH": false,
            "ALWAYS_REDIRECT_HOMEPAGE_TO_DASHBOARD_FOR_AUTHENTICATED_USER": true,
            "course_email_from_addr": "noreply@epfl.ch",
            "SESSION_COOKIE_DOMAIN": ".edx-test.phzh.ch.localhost",
            "css_overrides_file":  "edx-test.phzh.ch/css/style.css",
            "favicon_path": "edx-test.phzh.ch/images/favicon.ico",

            "COURSE_ABOUT_VISIBILITY_PERMISSION": "see_about_page",
            "COURSE_CATALOG_VISIBILITY_PERMISSION": "see_in_catalog",
            "ENABLE_PAID_COURSE_REGISTRATION": false,
            "ENABLE_SHOPPING_CART": false,
            "PLATFORM_NAME": "PHZH Moocs",
            "email_from_address": "noreply@epfl.ch"
        },
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
```

- Start LMS/CMS under edxapp user

```

paver devstack lms [--fast]
paver devstack studio [--fast]

```

- Open site http://edx-test.phzh.ch.localhost:8000/
