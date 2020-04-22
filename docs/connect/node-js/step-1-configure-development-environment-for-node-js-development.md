---
title: "Passaggio 1: Configurare l'ambiente di sviluppo per Node.js"
description: È necessario configurare l'ambiente di sviluppo con i prerequisiti per sviluppare un'applicazione che usa il driver Node.js per SQL Server.
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 38337772d9ec9db2503637122d0d1b616dc6ef5f
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528135"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>Passaggio 1:  Configurare l'ambiente di sviluppo per lo sviluppo Node.js
È necessario configurare l'ambiente di sviluppo con i prerequisiti per sviluppare un'applicazione che usa il driver Node.js per SQL Server.  Sebbene il metodo più comune consista nell'usare la gestione pacchetti del nodo (npm) per installare il modulo tedious, è anche possibile scaricarlo direttamente da [GitHub](https://github.com/pekim/tedious).  
  
Il driver Node.js usa il protocollo TDS che è abilitato per impostazione predefinita in SQL Server e nel database SQL di Azure.  Non è richiesta alcuna configurazione aggiuntiva.  
  
## <a name="windows"></a>Windows  
  
1. **Installare il runtime Node.js e la gestione pacchetti npm.**  
a. Passare a [Node.js](https://nodejs.org/en/download/)  
b. Fare clic sul collegamento MSI di Windows Installer.   
c. Al termine del download, eseguire il file con estensione msi per installare Node.js  
  
2. **Aprire cmd.exe**  
  
3. **Creare una directory di progetto** e passare alla directory.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **Creare un progetto Node.**  Per mantenere le impostazioni predefinite durante la creazione del progetto, premere INVIO fino a quando non viene creato il progetto. Al termine di questo passaggio, nella directory del progetto dovrebbe essere visualizzato un file package.json.  
```  
> npm init  
```  
  
5. **Installare il modulo tedious nel progetto.**  Il modulo Tedious è l'implementazione del protocollo TDS usato per comunicare con SQL Server.  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **Aprire il terminale**  
  
2. **Installare il runtime Node.js.**  
```  
>sudo apt-get install node  
```  
3. **Installare npm (gestione pacchetti del nodo).**  
```  
> sudo apt-get install npm  
```  
4. **Creare una directory di progetto** e passare alla directory.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **Creare un progetto Node.**  Per mantenere le impostazioni predefinite durante la creazione del progetto, premere INVIO fino a quando non viene creato il progetto. Al termine di questo passaggio, nella directory del progetto dovrebbe essere visualizzato un file package.json.  
```  
> sudo npm init  
```  
  
6. **Installare il modulo tedious nel progetto.**  Il modulo Tedious è l'implementazione del protocollo TDS usato per comunicare con SQL Server.  
```  
> sudo npm install tedious  
```  
  
## <a name="macos"></a>macOS  
  
1. **Installare il runtime Node.js e la gestione pacchetti npm.**  
a. Passare a [Node.js](https://nodejs.org/en/download/)  
b. Fare clic sul collegamento del programma di installazione macOS appropriato.  
c. Al termine del download, eseguire il file con estensione dmg per installare Node.js  
  
2. **Aprire il terminale**  
  
3. **Creare una directory di progetto** e passare alla directory.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **Creare un progetto Node.**  Per mantenere le impostazioni predefinite durante la creazione del progetto, premere INVIO fino a quando non viene creato il progetto. Al termine di questo passaggio, nella directory del progetto dovrebbe essere visualizzato un file package.json.  
```  
> npm init  
```  
  
5. **Installare il modulo tedious nel progetto.**  Si tratta dell'implementazione del protocollo TDS usato dal driver per comunicare con SQL Server.  
```  
> npm install tedious  
```  
