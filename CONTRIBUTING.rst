#########################
Contributing to testinfra
#########################

First, thanks for contributing to testinfra and make it even more awesome !

Pull requests
=============

Regardless the review by a developer, a pull request will trigger automatic
tests on https://travis-ci.org/philpep/testinfra/

You're encouraged to setup a full test environment, to add tests and check if
all the tests pass *before* submitting your pull request. To run the complete
test suite you must install:

- `Vagrant <https://vagrantup.com>`_ version 1.7 or greater
- `Docker <https://www.docker.com>`_ version 1.7 or greater
- `tox <https://tox.readthedocs.org/en/latest/>`_

To run all tests run::

    vagrant up --provider=docker
    tox

To run only some selected tests::

    # Only tests matching 'ansible' on 4 processes with pytest-xdist
    tox -- -v -n 4 -k ansible

    # Only jessie tests on python 2.7 and spawn a pdb on error
    tox -e py27 -- -v --pdb testinfra/test/integration/test_jessie.py


To speedup the docker images generation during `vagrant up` you can download
them before running the tests (docker will detect they are the same and use the
cache)::

    for tag in debian_jessie debian_wheezy centos_7 fedora_21 ubuntu_trusty; do
        docker pull philpep/testinfra:$tag
    done


Code style
==========

Your code must pass without errors under `flake8
<https://flake8.readthedocs.org>`_ with the extension `hacking
<http://docs.openstack.org/developer/hacking/>`_::


    pip install hacking
    flake8 testinfra
