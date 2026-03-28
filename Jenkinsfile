node {
    def appDir = '/var/www/nextjs-app'

    stage('Clean Workspace'){
        echo 'Cleaning Jenkins Workspace'
        deleteDir()
    }

    stage('Clone Repo'){
        echo 'Cloning the repo'
        git(
            branch: 'main',
            url: 'https://github.com/ujjwalsaini45/New-Devops-project.git'
        )
    }

    stage('Deploy'){
        echo 'Deploying app'
        sh """
            sudo mkdir -p ${appDir}
            sudo chown -R jenkins:jenkins ${appDir}

            rsync -av --delete --exclude='.git' --exclude='node_modules' ./ ${appDir}

            cd ${appDir}
            npm install
            npm run build

            pm2 delete nextjs-app || true
            pm2 start npm --name "nextjs-app" -- start
            pm2 save
        """
    }
}