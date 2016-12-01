Heroku Stack Images
=========

The provided `bin/cedar-14.sh` is the basis of a cedar stack image.

    cd stack-images
    vagrant up
    vagrant ssh

    sudo /vagrant/bin/build-stack 14.4.0 /vagrant/bin/cedar-14.sh
    -----> Starting build
    -----> Installing build tools
           Hit http://us.archive.ubuntu.com lucid Release.gpg
           ...
    -----> Cleaning up. Logs in /tmp/log/build-stack.log

    sudo /vagrant/bin/capture-stack 14.4.0
    -----> Starting capture
    -----> Creating image file /tmp/cedar64-14.4.0.img
           24+0 records in
           ...
    -----> Cleaning up. Logs in /tmp/log/capture-stack.log

    sudo /vagrant/bin/install-stack /tmp/cedar64-14.4.0.img.gz
    -----> Starting install
    -----> Gunzipping image /tmp/cedar64-14.4.0.img.gz
    -----> Mounting image /mnt/stacks/cedar64-14.4.0

Stack images are generally pushed to S3 and installed from there.

    sudo /vagrant/bin/push-stack 14.4.0 stacks_bucket \
      AWS_ACCESS_KEY_ID=xxx AWS_SECRET_ACCESS_KEY=xxx
    -----> Starting push
    -----> Uploading files
           /tmp/cedar64-14.4.0.img.gz -> s3://stacks_bucket/cedar64-14.4.0.img.gz
           ...

    sudo /vagrant/bin/install-stack \
      "http://s3.amazonaws.com/noah_herokustacks/cedar64-14.4.0.img.gz?AWS..."
    -----> Starting install
    -----> Downloading and gunzipping image
    -----> Mounting image /mnt/stacks/cedar64-14.4.0