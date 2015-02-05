Updating blog Manually:

    git add .
    git commit -m "Updated ..."
    git push origin draft

    rm -rf compiled
    ruhoh compile
    cd compiled
    touch CNAME
    echo "feveroftime.com" > CNAME
    git init
    git add .
    git commit -m "Update Blog"
    git push https://github.com/slamice/slamice.github.io.git master:master --force