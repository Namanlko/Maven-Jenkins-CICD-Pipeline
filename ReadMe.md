# 🚀 Jenkins CI/CD Pipeline for Maven Web Application

## 📌 Overview

This project implements a **Jenkins Declarative CI/CD Pipeline** for a Maven-based Java web application.

* Builds a Maven web app
* Runs tests **in Parallel**
* Stores WAR using **Stash/Unstash**
* Deploys to **Dev or Prod** based on a parameter
* Requires **Manual Approval for Prod**

## ⚙️ Pipeline Work Flow

1️⃣ **Build**

* Runs `mvn clean package -DskipTests=true`
* Loads `script.groovy`

2️⃣ **Parallel Tests**

* `testA` + `testB`
* On success → stash WAR from `webapp/target/`

3️⃣ **Deploy Dev**

* Runs when `select_environment = dev`
* Unstashes WAR → extracts to `/var/www/html`

4️⃣ **Deploy Prod**

* Runs when `select_environment = prod`
* **Manual approval required**
* Deploys to `/var/www/html` on `ProdServer`

## 🧠 Key Points

* **Parameter**

  * `select_environment = dev | prod`
* **Nodes**

  * Build/Test/Dev → `DevServer`
  * Prod → `ProdServer`
* **beforeAgent true**

  * Condition check happens **before** agent allocation
* **stash/unstash**

  * Artifact reuse — no rebuild needed

## ✅ Requirements

* Jenkins + Maven (`mymaven`)
* Java installed
* `/var/www/html` available on target servers
* Agents:

  * `DevServer`
  * `ProdServer`


## 🌊 Optional

Use **Blue Ocean** for better pipeline visualization.
