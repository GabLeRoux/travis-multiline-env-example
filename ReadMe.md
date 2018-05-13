# Travis-CI multiline env variables example

[![Build Status](https://travis-ci.com/GabLeRoux/travis-multiline-env-example.svg?branch=master)](https://travis-ci.com/GabLeRoux/travis-multiline-env-example)

I needed to generate a file based on an environment variable which contains a multiple lines. Note: `gitlab-ci` does support this out of the boxs. I just needed to do the same with Travis.

## The solution

As described in [travis-ci#7715](https://github.com/travis-ci/travis-ci/issues/7715#issuecomment-362536708), we can replace end lines by `\n` and wrap the environment variable in settings with `"$(echo -e '` and `')"`.

### Example:

Expected content

```xml
<?xml version="1.0" encoding="UTF-8"?><root>
    <Example id"hello">
        <Test />
    </Example>
</root>
```

The above content with endlines replaced:

```xml
<?xml version="1.0" encoding="UTF-8"?><root>\n    <Example id"hello">\n        <Test />\n    </Example>\n</root>
```

What we actually need to add in Travis environment variables settings:

```xml
"$(echo -e '<?xml version="1.0" encoding="UTF-8"?><root>\n    <Example id"hello">\n        <Test />\n    </Example>\n</root>')"
```

:white_check_mark: [Confirmed working here](https://travis-ci.com/GabLeRoux/travis-multiline-env-example)
