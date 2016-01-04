Composer Asset Installer
========================

This is a little helper that eases the usage of assets through composer.
It copies configured assets (individual files or directories) from the vendor 
folder to specified directories in your application.

Usage
-----
### Require this package in your composer.json file
```
    "require": {
        ...
        "risrc/asset-installer": "*"
    },
```
### Add `post-package-install` and `post-package-update` hooks
```
    "scripts": {
        ...
        "post-package-install": [
            "RiSrc\\Composer\\Scripts\\AssetInstallerScript::postPackageInstall"
        ],
        "post-package-update": [
            "RiSrc\\Composer\\Scripts\\AssetInstallerScript::postPackageUpdate"
        ]
    },
```
### Configure your assets
```
    "extra": {
        ...
        "asset-installer": {
            "path-config": {
                ...
            },
            "assets": {
                ...
            }
        }
    }
```

Configuration
-------------
A note for [Compass](http://compass-style.org/) users:
The path configuration from your compass config file is applied automatically,
if you can execute `compass config -p <compass property>` where composer is executed .

### Available placeholders
- `{{LIBRARY_NAME}}`      will be replaced with the package name without vendor prefix
- `{{BASE_PATH}}`         can be configured with `base-path` (defaults to Compass property `project_path`)
- `{{JS_PATH}}`           can be configured with `js-path` (defaults to Compass property `javascripts_path`)
- `{{CSS_PATH}}`          can be configured with `css-path` (defaults to Compass property `css_path`)
- `{{SASS_PATH}}`         can be configured with `sass-path` (defaults to Compass property `sass_path`)
- `{{FONTS_PATH}}`        can be configured with `fonts-path` (defaults to Compass property `fonts_path`)
- `{{IMAGE_PATH}}`        can be configured with `image-path` (defaults to Compass property `images_path`)
- `{{LIB_PATH}}`          can be configured with `lib-path` (defaults to `lib/{{LIBRARY_NAME}}`)
- `{{JS_LIB_PATH}}`       can be configured with `js-lib-path` (defaults to `{{JS_PATH}}/{{LIB_PATH}}`)
- `{{CSS_LIB_PATH}}`      can be configured with `css-lib-path` (defaults to `{{CSS_PATH}}/{{LIB_PATH}}`)
- `{{SASS_LIB_PATH}}`     can be configured with `sass-lib-path` (defaults to `{{SASS_PATH}}/{{LIB_PATH}}`)
- `{{FONTS_LIB_PATH}}`    can be configured with `fonts-lib-path` (defaults to `{{FONTS_PATH}}/{{LIB_PATH}}`)
- `{{IMAGE_LIB_PATH}}`    can be configured with `image-lib-path` (defaults to `{{IMAGE_PATH}}/{{LIB_PATH}}`)

### Override default path config (optional)
```
    "extra": {
        "asset-installer": {
            "path-config": {
                "lib-path": "vendor/{{LIBRARY_NAME}}"
            }
        }
    }
```

### Configure your assets
```
    "extra": {
        "asset-installer": {
            "assets": {
                "<package_name>": {
                    "<source_path>": "<target_path>"
                },
                "components/jquery": {
                    "jquery.min.js": "{{JS_PATH}}"
                },
                "zurb/foundation": {
                    "scss": "assets/foundation/scss",
                    "js": "{{JS_LIB_PATH}}",
                    "dist/foundation.min.js": "{{JS_PATH}}",
                    "dist/foundation.min.css": "{{CSS_PATH}}"
                }
            }
        }
    }
```

License
-------
See [LICENSE](LICENSE)
