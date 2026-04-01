sh """
    sudo mkdir -p ${appDir}
    sudo chown -R jenkins:jenkins ${appDir}

    rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}

    cd ${appDir}

    sudo rm -rf .next

    npm install
    npm run build

    /usr/bin/pm2 delete nextjs-app || true
    /usr/bin/pm2 start npm --name "nextjs-app" -- start
"""