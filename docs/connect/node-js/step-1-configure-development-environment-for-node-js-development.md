---
title: "Passaggio 1: Configurare l'ambiente di sviluppo per lo sviluppo Node.js | Microsoft Docs"
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68003755"
---
# <a name="step-1--configure-development-environment-for-nodejs-development"></a>Passaggio 1: Configurare l'ambiente di sviluppo per lo sviluppo Node.js
È necessario configurare l'ambiente di sviluppo con i prerequisiti per sviluppare un'applicazione che usa il driver node. js per SQL Server.  Il metodo più comune consiste nell'usare node Package Manager (NPM) per installare il modulo noioso, ma è possibile scaricare il modulo noioso direttamente su [GitHub](https://github.com/pekim/tedious) , se si preferisce.  
  
Si noti che il driver node. js usa il protocollo TDS, che è abilitato per impostazione predefinita in SQL Server e nel database SQL di Azure.  Non è richiesta alcuna configurazione aggiuntiva.  
  
## <a name="windows"></a>Windows  
  
1. **Installare il runtime di node. js e gestione pacchetti NPM**  
A. Vai a [node. js](https://nodejs.org/en/download/)  
B. Fare clic sul collegamento MSI di Windows Installer appropriato.   
c. Una volta scaricata, eseguire il file MSI per installare Node. js  
  
2. **Apri cmd. exe**  
  
3. **Creare una directory del progetto** e passare a tale directory.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
4. **Creare un progetto node.**  Per mantenere le impostazioni predefinite durante la creazione del progetto, premere INVIO fino a quando non viene creato il progetto. Al termine di questo passaggio, nella directory del progetto dovrebbe essere visualizzato un file Package. JSON.  
```  
> npm init  
```  
  
5. **Installare il modulo noioso nel progetto.**  Si tratta dell'implementazione del protocollo TDS utilizzato dal driver per comunicare con SQL Server.  
```  
> npm install tedious  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1.  **Apri terminale**  
  
2. **Installare il runtime di node. js**  
```  
>sudo apt-get install node  
```  
3. **Installare NPM (gestione pacchetti di nodi)**  
```  
> sudo apt-get install npm  
```  
4. **Creare una directory del progetto** e passare a tale directory.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
5. **Creare un progetto node.**  Per mantenere le impostazioni predefinite durante la creazione del progetto, premere INVIO fino a quando non viene creato il progetto. Al termine di questo passaggio, nella directory del progetto dovrebbe essere visualizzato un file Package. JSON.  
```  
> sudo npm init  
```  
  
6. **Installare il modulo noioso nel progetto.**  Si tratta dell'implementazione del protocollo TDS utilizzato dal driver per comunicare con SQL Server.  
```  
> sudo npm install tedious  
```  
  
## <a name="mac"></a>Mac  
  
1. **Installare il runtime di node. js e gestione pacchetti NPM**  
A. Vai a [node. js](https://nodejs.org/en/download/)  
B. Fare clic sul collegamento Mac OS Installer appropriato.  
c. Una volta scaricata, eseguire il DMG per installare Node. js  
  
2. **Apri terminale**  
  
3. **Creare una directory del progetto** e passare a tale directory.    
```  
> mkdir HelloWorld  
> cd HelloWorld  
```  
  
4. **Creare un progetto node.**  Per mantenere le impostazioni predefinite durante la creazione del progetto, premere INVIO fino a quando non viene creato il progetto. Al termine di questo passaggio, nella directory del progetto dovrebbe essere visualizzato un file Package. JSON.  
```  
> npm init  
```  
  
5. **Installare il modulo noioso nel progetto.**  Si tratta dell'implementazione del protocollo TDS utilizzato dal driver per comunicare con SQL Server.  
```  
> npm install tedious  
```  
  
