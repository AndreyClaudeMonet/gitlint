We'd love for you to contribute to gitlint. Thanks for your interest!
Sometimes it takes a while for [me](https://github.com/jorisroovers) to
get back to you (this is a hobby project), but rest assured that we read your message and appreciate your interest!
We maintain a [wishlist on our wiki](https://github.com/jorisroovers/gitlint/wiki/Wishlist),
but we're obviously open to any suggestions!

# Guidelines

When contributing code, please consider all the parts that are typically required:

- [Unit tests](https://github.com/jorisroovers/gitlint/tree/master/gitlint/tests) (automatically
  [enforced by Travis](https://travis-ci.org/jorisroovers/gitlint)). Please consider writing
  new ones for your functionality, not only updating existing ones to make the build pass.
- [Integration tests](https://github.com/jorisroovers/gitlint/tree/master/qa) (also automatically
  [enforced by Travis](https://travis-ci.org/jorisroovers/gitlint)). Again, please consider writing new ones
  for your functionality, not only updating existing ones to make the build pass.
- [Documentation](https://github.com/jorisroovers/gitlint/tree/master/docs)

Since we want to maintain a high standard of quality, all of these things will have to be done regardless before code
can make it as part of a release. If you can already include them as part of your PR, it's a huge timesaver for us
and it's likely that your PR will be merged and released a lot sooner. Thanks!
# Development #

There is a Vagrantfile in this repository that can be used for development.
```bash
vagrant up
vagrant ssh
```

Or you can choose to use your local environment:

```bash
virtualenv .venv
pip install -r requirements.txt -r test-requirements.txt -r doc-requirements.txt
python setup.py develop
```

To run tests:
```bash
./run_tests.sh                       # run unit tests and print test coverage
./run_test.sh gitlint/tests/test_body_rules.py::BodyRuleTests::test_body_missing # run a single test
./run_tests.sh --no-coverage         # run unit tests without test coverage
./run_tests.sh --integration         # Run integration tests (requires that you have gitlint installed)
./run_tests.sh --build               # Run build tests (=build python package)
./run_tests.sh --pep8                # pep8 checks
./run_tests.sh --stats               # print some code stats
./run_tests.sh --git                 # inception: run gitlint against itself
./run_tests.sh --lint                # run pylint checks
./run_tests.sh --all                 # Run unit, integration, pep8 and gitlint checks
```

The ```Vagrantfile``` comes with ```virtualenv```s for python 2.6, 2.7, 3.3, 3.4, 3.5, 3.6 and pypy2.
You can easily run tests against specific python environments by using the following commands *inside* of the Vagrant VM:
```
./run_tests.sh --envs 26               # Run the unit tests against Python 2.6
./run_tests.sh --envs 27,33,pypy2      # Run the unit tests against Python 2.7, Python 3.3 and Pypy2
./run_tests.sh --envs 27,33 --pep8     # Run pep8 checks against Python 2.7 and Python 3.3 (also works for ```--git```, ```--integration```, ```--pep8```, ```--stats``` and ```--lint```).
./run_tests.sh --envs all --all        # Run all tests against all environments
./run_tests.sh --all-env --all         # Idem: Run all tests against all environments
```

!!! important
    Gitlint commits and pull requests are gated on all of our tests and checks.

# Packaging #

To see the package description in HTML format
```
pip install docutils
export LC_ALL=en_US.UTF-8
export LANG=en_US.UTF-8
python setup.py --long-description | rst2html.py > output.html
```

# Documentation #
Outside the vagrant box (on your host machine):
```bash
mkdocs serve
```

Then access the documentation website on your host machine on [http://localhost:8000]().
Note that this is only supported for python >= 2.7.
