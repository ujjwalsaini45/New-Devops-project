node {

    def appDir = '/var/www/nextjs-app'

    stage('Clean Workspace') {
        echo 'Cleaning workspace'
        deleteDir()
    }

    stage('Clone Repo') {
        echo 'Cloning repository'
        git branch: 'main',
            url: 'https://github.com/ujjwalsaini45/New-Devops-project'
    }

    stage('Deploy') {
        echo 'Deploying app'
        sh """
            # Create directory
            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}

            # Copy files
            rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}

            cd ${appDir}

            # Clean old build
            sudo rm -rf .next

            # Install dependencies
            npm install

            # Build Next.js app
            npm run build

            # Restart app using PM2
            pm2 delete nextjs-app || true
            pm2 start npm --name "nextjs-app" -- start
        """
    }
}