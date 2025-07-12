#### 3. Buat file buildspec.yml
Buka project pada Visual Studio Code:

Buat file baru dengan nama buildspec.yml di root folder proyek:

```bash
version: 0.2

phases:
  install:
    runtime-versions:
      php: 8.1
    commands:
      - echo "📦 Installing dependencies..."
      - curl -sS https://getcomposer.org/installer | php
      - php composer.phar install --no-dev
  pre_build:
    commands:
      - echo "🔐 Setting up SSH private key"
      - echo "$EC2_PRIVATE_KEY" > ec2-key.pem
      - chmod 400 ec2-key.pem
  build:
    commands:
      - echo "✅ Running unit tests..."
      - ./vendor/bin/phpunit
  post_build:
    commands:
      - echo "🚀 Deploying to EC2..."
      - rsync -avz -e "ssh -o StrictHostKeyChecking=no -i ec2-key.pem" ./ ec2-user@$EC2_HOST:/var/www/html/
artifacts:
  files:
    - '**/*'
```


