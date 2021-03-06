------
EC2RDP
------

.. image:: https://img.shields.io/pypi/v/ec2rdp.svg
    :target: https://pypi.python.org/pypi/ec2rdp

.. image:: https://travis-ci.org/jtvsoftwares/ec2rdp.svg?branch=master
    :target: https://travis-ci.org/jtvsoftwares/ec2rdp

.. image:: https://coveralls.io/repos/github/jtvsoftwares/ec2rdp/badge.svg?branch=master
    :target: https://coveralls.io/github/jtvsoftwares/ec2rdp?branch=master

.. image:: https://img.shields.io/pypi/l/ec2rdp.svg
    :target: https://github.com/jtvsoftwares/ec2rdp/blob/master/LICENSE

.. image:: https://img.shields.io/pypi/pyversions/ec2rdp.svg
    :target: https://github.com/jtvsoftwares/ec2rdp

Summary
-------
Simple command line utility to decrypt the password of an
AWS EC2 windows instance, put the decrypted password in
the clipboard and write an rdp file to access the AWS
EC2 windows instance.

Install
-------
::

    pip install ec2rdp

Usage
-----
::

    ec2rdp [-h] [-o OUTPUT] [-k KEY] [-q] [--aws-profile AWS_PROFILE]
           [--aws-access-key-id AWS_ACCESS_KEY_ID]
           [--aws-secret-access-key AWS_SECRET_ACCESS_KEY]
           [--aws-region AWS_REGION]
           instance-id

    positional arguments:
      instance-id           The instance-id to decrypt the password.

    optional arguments:
      -h, --help            show this help message and exit
      -o OUTPUT, --output OUTPUT
                            The path for the rdp file to be created.
      -k KEY, --key KEY     The path to the private key file to decrypt the
                            password.
      -q, --quick           The script will not ask for the passphrase for the key
                            file.
      --aws-profile AWS_PROFILE
                            The profile name for aws credentials
      --aws-access-key-id AWS_ACCESS_KEY_ID
                            The access key id for aws
      --aws-secret-access-key AWS_SECRET_ACCESS_KEY
                            The secret access key for aws
      --aws-region AWS_REGION
                            The region for aws

AWS Credentials
---------------
The script will look for credentials to AWS in the following locations:

- ``AWS_PROFILE`` environment variable with credentials set in either ``~/.aws/credentials`` or ``~/.aws/config``. When using this, ``--aws-region`` must be set, ``~/.aws/config`` must contain a region value for the profile or ``AWS_DEFAULT_REGION`` must be set.
- ``AWS_ACCESS_KEY_ID``, ``AWS_SECRET_ACCESS_KEY`` environment variables. When using this, ``--aws-region`` must be set or ``AWS_DEFAULT_REGION`` must be set.
- ``--aws-profile`` command line option. When using this, ``--aws-region`` must be set, ``~/.aws/config`` must contain a region value for the profile or ``AWS_DEFAULT_REGION`` must be set.
- ``--aws-access-key-id``, ``--aws-secret-access-key`` command line options. When using this, ``--aws-region`` must be set or ``AWS_DEFAULT_REGION`` must be set.

Key in AWS Config file
----------------------
If you are using the same key for all the AWS EC2 Windows instances available from a profile, you can set the path to
the key file in the ``~/.aws/config`` file. To do so, add a ``ec2rdp_key`` entry with the path to the key file under
the profile.

Example::

    [profile profile1]
    output = json
    region = us-west-1
    ec2rdp_key = ~/keys/profile1.pem
