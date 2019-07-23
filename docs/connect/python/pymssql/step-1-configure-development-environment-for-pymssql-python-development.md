---
title: "Passaggio 1: configurare l'ambiente di sviluppo Python per pymssql | Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5bf2942b79cf7e72efbb36a53019de8208cd3b8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67935820"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>Passaggio 1: Configurare l'ambiente di sviluppo per lo sviluppo Python con pymssql
È necessario configurare l'ambiente di sviluppo con i prerequisiti per sviluppare un'applicazione che usa il driver Python per SQL Server.    
  
Si noti che i driver SQL Python usano il protocollo TDS, che è abilitato per impostazione predefinita in SQL Server e nel database SQL di Azure.  Non è richiesta alcuna configurazione aggiuntiva.  
  
## <a name="windows"></a>Windows  
  
1. **Installare il runtime di Python e gestione pacchetti PIP**  
A. Vai a [Python.org](https://www.python.org/downloads/)  
B. Fare clic sul collegamento MSI di Windows Installer appropriato.   
c. Una volta scaricato, Esegui il file MSI per installare il runtime di Python  
  
2. **Scaricare il modulo pymssql** da [qui](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    Assicurarsi di scegliere il file WHL corretto.  Ad esempio, se si usa Python 2,7 in un computer a 64 bit scegliere: pymssql-2.1.1-CP27-None-win_amd64. WHL. Dopo aver scaricato il file con estensione WHL, inserirlo nella cartella C:/Python27.  
      
3. **Apri cmd. exe**  
  
4. **Installare il modulo pymssql**     
    Ad esempio, se si usa Python 2,7 in un computer a 64 bit:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Installare il runtime di Python e gestione pacchetti PIP**  Python è preinstallato nella maggior parte delle distribuzioni di Ubuntu.  Se nel computer non è installato Python, è possibile scaricare il tarball di origine da [Python.org](https://www.python.org/downloads/) e compilare localmente oppure è possibile usare Gestione pacchetti:  
```  
> sudo apt-get install python   
```  
  
2.  **Apri terminale**  
  
3.  **Installare il modulo e le dipendenze di pymssql**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **Installare il runtime di Python e gestione pacchetti PIP**  
A. Vai a [Python.org](https://www.python.org/downloads/)  
B. Fare clic sul collegamento Mac Installer appropriato.   
c. Una volta scaricato, Esegui il pacchetto pkg per installare il runtime di Python  
  
2.  **Apri terminale**  
  
3. **Installare Homebrew Package Manager**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **Installare il modulo FreeTDS**  
```  
> brew install FreeTDS  
```  
  
5.  **Installare il modulo pymssql**  
```  
> sudo -H pip install pymssql  
```
