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
