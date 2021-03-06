# Arrow library: How to run the website in your local server

## Steps

### 1. Prepare the site

```
git clone https://github.com/arrow-kt/arrow-site.git
cd arrow-site
./gradlew runAnk
```

Then `build/site` will be created.

### 2. Copy API Doc from Arrow library

They were created by the steps included in [How to generate and validate the documentation](how-to-generate-and-validate-documentation.md):

```
cd <arrow-library-repository>
./gradlew clean dokka
./gradlew :arrow-docs:runAnk
```

and then:

```
cp -r <arrow-library-repository>/arrow-docs/build/site/* arrow-site/build/site/
```

### 3. Run the website in your local server

```bash
cd arrow-site
bundle install --gemfile Gemfile --path vendor/bundle
bundle exec jekyll serve -s build/site/
```

This will install any needed dependencies locally, and will use it to launch the complete website in [127.0.0.1:4000](http://127.0.0.1:4000) so you can open it with a standard browser.

If you get an error while installing the Ruby gem _http_parser_, check if the path to your Arrow directory contains spaces. According to this [issue](https://github.com/tmm1/http_parser.rb/issues/47), the installation with spaces in the path is currently not working.

## How to test links

Test for broken links in documentation using

```sh
wget --spider -r -nd -nv -l 5 http://127.0.0.1:4000/docs/
```
