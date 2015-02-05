Updating blog Manually:

    git add .
    git commit -m "Updated ..."
    git push origin draft

    ruhoh compile
    cd compiled
    touch CNAME
    echo "feveroftime.com" > CNAME
    git init
    git add .
    git commit -m "Update Blog"
    git push https://github.com/slamice/slamice.github.io.git master:master --force
    rm -rf compiled