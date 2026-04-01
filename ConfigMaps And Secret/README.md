# Kuberneties Configmap And Secret 
---
## Introduction
### What is a ConfigMap?
A **ConfigMap** is a Kubernetes resource used to store non-confidential data as key-value pairs. It helps decouple configuration data from application code.

### What is a Secret?
A **Secret** is a Kubernetes resource designed to store confidential data, such as passwords or API keys, in a secure and encoded format. Secrets are encoded using Base64, providing a layer of obfuscation but not encryption.

---
## Why Use ConfigMap and Secret?
 - **Separation of Concerns**: Decouples configuration from application logic.
 - **Ease of Updates**: Configuration changes do not require rebuilding or redeploying applications.
 - **Security**: Secrets ensure sensitive data is handled securely.
