#### 3. Buat file buildspec.yml
a. Buka project pada Visual Studio Code:

b. Buat file baru dengan nama buildspec.yml di root folder proyek:

```bash
version: 0.2

phases:
  install:
    runtime-versions:
      php: 8.1
    commands:
      - echo "📦 Installing dependencies..."

  pre_build:
    commands:
      - echo "🔐 Setting up SSH private key"

  build:
    commands:
      - echo "✅ Running unit tests..."

  post_build:
    commands:
      - echo "🚀 Deploying to EC2..."

artifacts:
  files:
    - '**/*'
```

c. Simpan kode pada file buildspec.yml

d. tambahkan pada git dengan perintah berikut:
```bash
git add buildspec.yml
```

e. Buat commit pada git dengan perintah berikut:
```bash
git commit -m "Create file buildspec.yml"
```

f. Push ke GitHub dengan perintah berikut:
```bash
git push -u origin main
```

#Buat connection

Masuk ke service CodeCommit

Disebelah kiri paling bawah klik Setings dan klik Connections

Create Connection

Select providernya GitHub dan masukkan nama connectionnya, dan connect to GitHub

Pada app instalations buat repository access menjadi all repositories, klik save

Kemudian connect

Masuk ke CodeBuild

Klik create project

Buat nama projectnya, source ubah menjadi github jika belum ada akun dikaitkan dulu akunnya, pilih "repository in my GitHub account" dan pilih repositorynya.

Build typenya single build

Pada Environment OS nya buat ubuntu, pada service rolenya buat new role jika belum punya role (buat permision policiesnya AmazonEC2RoleforAWSCodeDeploy)

Build specifications pilih Use a buildspec file dan masukkan namanya "buildspec.yml" (buat dulu filenya di vscode)

Artifact primarynya pilih "Amazon S3", dan pilih bucket name yang dibuat tadi

Klik Create build project

Masuk ke code deploy

Pilih application, dan creat application

Buat namanya dan platformnya pilih EC2, dan klik Create application
