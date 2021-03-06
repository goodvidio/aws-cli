This example shows how to encrypt the string ``"1\!2@3#4$5%6^7&8*9(0)-_=+"``
and save the binary contents to a file::

  aws kms encrypt --key-id my-key-id --plaintext "1\!2@3#4$5%6^7&8*9(0)-_=+" --query CiphertextBlob --output text | base64 -d > /tmp/encrypted

If you are on Mac OS X, you'll need to use ``base64 -D`` instead of
``base64 -d`` to decode the base64 ciphertext blob.

If you want to decrypt the contents of the file above you can use this
command::

  echo "Decrypted is: $(aws kms decrypt --ciphertext-blob fileb:///tmp/encrypted  --output text --query Plaintext | base64 -d)"

On Mac OS X, you will again need to use ``base64 -D`` instead of ``base64 -d``.

Note the use of the ``fileb://`` prefix in the ``decrypt`` command above.  This
indicates that the referenced file contains binary contents, and that the file
contents are not decoded before being used.
