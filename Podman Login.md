
# ✅ Podman Login Configuration Steps

Follow these steps to configure and authenticate Podman with your private container registry.

---

## 🛠️ Step 1: Install Container Tools

```bash
yum install container-tools -y
```

---

## 📁 Step 2: Create Config Directory

```bash
mkdir -p .config/containers && cd $_
```

---

## ✏️ Step 3: Edit registries.conf File

```bash
vim registries.conf
```

Add the following content to the file:

```toml
unqualified-search-registries = ["registry.lab.example.com"]

[[registry]]
location = "registry.lab.example.com"
insecure = true
blocked = false
```

---

## 📋 Step 4: Verify Podman Installation

```bash
podman info
```

---

## 🔐 Step 5: Login to the Registry

```bash
podman login registry.lab.example.com
```

Use the following credentials:

```makefile
Username: admin
Password: redhat321
```

---

✅ Now you're ready to use Podman with your custom container registry.
