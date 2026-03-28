stage('Deploy'){
    echo 'Deploying app'
    sh """
        sudo mkdir -p ${appDir}
        sudo chown -R jenkins:jenkins ${appDir}

        rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}

        cd ${appDir}

        # Fix permissions
        sudo rm -rf .next
        sudo chown -R jenkins:jenkins ${appDir}

        # Install & build WITHOUT sudo
        npm install
        npm run build

        pm2 delete nextjs-app || true
        pm2 start npm --name "nextjs-app" -- start
    """
}