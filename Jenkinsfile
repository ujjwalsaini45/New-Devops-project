node {

    def appDir = '/var/www/nextjs-app'

    stage('Deploy'){
        echo 'Deploying app'
        sh """
            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}

            rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}

            cd ${appDir}

            sudo rm -rf .next
            sudo chown -R jenkins:jenkins ${appDir}

            npm install
            npm run build

            pm2 delete nextjs-app || true
            pm2 start npm --name "nextjs-app" -- start
        """
    }
}