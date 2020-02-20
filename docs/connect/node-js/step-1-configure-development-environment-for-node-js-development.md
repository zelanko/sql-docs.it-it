---
title: "Passaggio 1:  Configurare l'ambiente di sviluppo per lo sviluppo Node.js | Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 2dad01f1-fadf-4ac9-9b4d-26be3d301886
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bce89cc12c7493522de55adffb69fcbe3307cbdf
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "68003755"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>Passaggio 1:  Configurare l'ambiente di sviluppo per lo sviluppo Node.js
È necessario configurare l'ambiente di sviluppo con i prerequisiti per sviluppare un'applicazione che usa il driver Node.js per SQL Server.  Sebbene il metodo più comune consista nell'usare la gestione pacchetti del nodo (npm) per installare il modulo tedious, è anche possibile scaricarlo direttamente da [GitHub](https://github.com/pekim/tedious).  
  
Si noti che il driver Node.js usa il protocollo TDS che è abilitato per impostazione predefinita in SQL Server e nel database SQL di Azure.  Non è richiesta alcuna configurazione aggiuntiva.  
  
## <a name="windows"></a>Windows  
  
1. **Installare il runtime Node.js e la gestione pacchetti npm**  
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
  
5. **Installare il modulo tedious nel progetto.**  Si tratta dell'implementazione del protocollo TDS usato dal driver per comunicare con SQL Server.  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **Aprire il terminale**  
  
2. **Installare il runtime Node.js**  
```  
>sudo apt-get install node  
```  
3. **Installare npm (gestione pacchetti del nodo)**  
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
  
6. **Installare il modulo tedious nel progetto.**  Si tratta dell'implementazione del protocollo TDS usato dal driver per comunicare con SQL Server.  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **Installare il runtime Node.js e la gestione pacchetti npm**  
a. Passare a [Node.js](https://nodejs.org/en/download/)  
b. Fare clic sul collegamento del programma di installazione Mac OS appropriato.  
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
  
