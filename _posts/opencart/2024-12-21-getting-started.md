---
layout: post
title: "Getting Started"
date: 2024-12-21 00:00:00 -0000
categories: [opencart]
tags: [opencart, installation]
---

## Download Opencart
Visit [this page](https://www.opencart.com/index.php?route=cms/download/history) and download opencart version **3.0.4.0**

## Download Journal
Visit [this page](https://v32.journal-theme.com/download/)
In the section where credentials are needed use: 

Themeforest User: **mental1993**

Purchase Code: **150d89be-0c8c-4785-b644-1a7d06075ea7**

Download journal version **Journal_Theme_3.x.x** without the assets (the first choice)

## 📓 Create Gitlab Project
- Visit [Gitlab](http://git.dtek.gr/) and press **New Project**
- **Create Blank Project**
- Fill in project details
- Set visibility to **Private**
- Set invite to **Maintainer**

## 🛒 Install Opencart
- Create a new project folder in your web-server(XAMPP, MAMP, etc) projects folder and name it after your project
- Unzip the opencart file you downloaded earlier
- Paste the contents of upload inside your project folder
- Create a database in your localhost server. The database should have the following specifications:
  - *utf8mb4_general_ci* encoding
  - SQL *8.0* version
- Open the project in your localhost adress
- Follow the steps shown in the tutorial
- When finished, delete the *install* folder and the *php.ini* file

## 📝 Install Journal
- Unzip *JOURNAL_3.2.0-rc.39*
- Open the folder named Opencart_3.x
- Move the files inside in the correspondig files of your project folder (if using a mac, you're going to need the *rsync* command described in dtek-shared-notes/Other/mac_useful_commands.md)
- Go to *Extensions->Themes* and press **install** in Journal
- Go to *System->Settings->General->Theme* and choose **Journal Theme**
-  Go to *Extensions->Modifications* and press **Refresh Modifications**
-  Go to *Journal->Dashboard* and fill in the credentials in the **Licenses** section


## 🖥 Import Demo
- Visit the [journal website](https://www.journal-theme.com/) and choose a demo (usually here in dtek we choose the 9th demo)
  - Login to the demo admin (username and password is *demo*)
  - Go to *Journal->System->Import/Export* and press the button in the *Actions* after filling the credentials again
- Go back to your project
  - Go to *Journal->System->Import/Export* and this time choose **Import**

## 🧹 Some Cleanup
- Go to the folder of the project to *system->storage* and cleanup each folder by following instructions:
  - **cache**: Delete everything EXCEPT *index.html*
  - **download**: Do NOT touch
  - **logs**: Delete everything EXCEPT *index.html*
  - **modification**: Delete everything EXCEPT *index.html*
  - **session**: Delete everything EXCEPT *index.html* (if there is an *htaccess* file you should also not delete it)
  - **upload**: Do NOT touch
  - **vendor**: Do NOT touch
- Go to *image->catalog->demo* and it's up to you if you want to delete something

## 🫂 Configure Git
- Copy a *.gitignore* file from another project and paste it to the root folder of the project
- Initialize git version control system by the following commands:
``` bash
    git init
    git add .
    git commit -m "initial commit"
    git remote add origin http://gitlab.dtek.gr/...
    git push -u origin master
    git gc
```

## 🇬🇷 Greek Language
- Go to [this page](https://git.dtek.gr/opencart/extensions/greek-language) and download it.
- Transfer the files from the *upload* folder to the corresponding project files
- Navigate to *catalog/language/el-gr/mail* and create a **register.php** file. You can copy that file from a previous project.
- Go to *Extensions->Modifications* and press **Refresh Modifications**
- Navigate in your page to *System->Localisation->Languages*, press **Add new** and fill in:
  - Language name: Greek
  - Code: el-gr
  - Locale: el-GR,el_GR.UTF-8,el_GR,el-gr,greek
  - Status: Enabled
- Run the .sql file you downloaded. **NOTE**: Replace the database table prefixes with the correct one.
- To set greek as default follow navigate to *System->Settings->Local* and change Language to greek
- Navigate to *System->Localisation->Currencies* and delete every other currency except **Euro**
- Edit **Euro** and set the *Value* field to 1
- You also need to go to *catalog/conteroller/startup/startup.php* and search the `if (isset($this->session->data['language']))` statement and add an else condition like the following: 
```php
} else {
  $code = 'el-gr';
}
```

## 🧩 Go-to Opencart Plugins
- File Manager Pro
- GDPR
- Greek Translation 3.02
- Cash on Delivery fee 2.x
- Google RECaptcha v.3