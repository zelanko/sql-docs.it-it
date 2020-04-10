---
title: "Passaggio 1: Configurare l'ambiente di sviluppo Python pymssql | Microsoft Docs"
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 6d392a5e-b08e-4b35-9e99-61260888fc41
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3310f268bf04b015c5f80cd08b2ae3909fd3a5c2
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926809"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>Passaggio 1: Configurare l'ambiente di sviluppo per lo sviluppo Python con pymssql
È necessario configurare l'ambiente di sviluppo con i prerequisiti per sviluppare un'applicazione che usa il driver Python per SQL Server.    
  
Si noti che il driver Python usa il protocollo TDS che è abilitato per impostazione predefinita in SQL Server e nel database SQL di Azure.  Non è richiesta alcuna configurazione aggiuntiva.  
  
## <a name="windows"></a>Windows  
  
1. **Installare il runtime Python e Gestione pacchetti pip**  
a. Passare a [python.org](https://www.python.org/downloads/)  
b. Fare clic sul collegamento MSI di Windows Installer.   
c. Al termine del download, eseguire il file con estensione msi per installare il runtime Python  
  
2. **Scaricare il modulo pymssql** da [qui](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    Accertarsi di scegliere il file con estensione whl corretto.  Ad esempio: Se si usa Python 2.7 in un computer a 64 bit, scegliere: pymssql‑2.1.1‑cp27‑none‑win_amd64.whl. Una volta scaricato il file con estensione whl, posizionarlo nella cartella C:/Python27.  
      
3. **Aprire cmd.exe**  
  
4. **Installare il modulo pymssql**     
    Ad esempio, se si usa Python 2.7 in un computer a 64 bit:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Installare il runtime di Python e Gestione pacchetti pip** Python è preinstallato nella maggior parte delle distribuzioni di Ubuntu.  Se nel computer non è installato Python, è possibile scaricare il tarball di origine da [python.org](https://www.python.org/downloads/) e compilare localmente oppure è possibile usare la gestione pacchetti:  
```  
> sudo apt-get install python   
```  
  
2.  **Aprire il terminale**  
  
3.  **Installare il modulo pymssql e le dipendenze**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **Installare il runtime Python e Gestione pacchetti pip**  
a. Passare a [python.org](https://www.python.org/downloads/)  
b. Fare clic sul collegamento PKG del programma di installazione Mac appropriato.   
c. Al termine del download, eseguire il file con estensione pkg per installare il runtime Python  
  
2.  **Aprire il terminale**  
  
3. **Installare la gestione pacchetti Homebrew**  
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
