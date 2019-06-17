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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9d74e3ce2f7db91aca295dcb7507431a82e49c8c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803873"
---
# <a name="step-1-configure-development-environment-for-pymssql-python-development"></a>Passaggio 1: Configurare l'ambiente di sviluppo per lo sviluppo Python con pymssql
È necessario configurare l'ambiente di sviluppo con i prerequisiti per lo sviluppo di un'applicazione usando il Driver Python per SQL Server.    
  
Si noti che i driver SQL Python usano il protocollo TDS, che è abilitato per impostazione predefinita in SQL Server e Database SQL di Azure.  Non è richiesta alcuna configurazione aggiuntiva.  
  
## <a name="windows"></a>Windows  
  
1. **Installare il runtime di Python e gestione pacchetti pip**  
A. Passare a [python.org](https://www.python.org/downloads/)  
B. Fare clic sul collegamento appropriato Windows installer msi.   
c. Esegui una volta scaricato il file msi per installare il runtime di Python  
  
2. **Scaricare il modulo pymssql** da [qui](https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymssql)  
  
    Assicurarsi di che scegliere il file con estensione whl corretto.  Ad esempio: se si usa Python 2.7 su un computer a 64 bit scegliere: pymssql‑2.1.1‑cp27‑none‑win_amd64.whl. Una volta scaricato il file con estensione WhL inserirlo nella cartella c:/python27.  
      
3. **Aprire cmd.exe**  
  
4. **Installare pymssql modulo**     
    Ad esempio, se si usa Python 2.7 su un computer a 64 bit:  
```  
> cd c:\Python27  
> pip install pymssql‑2.1.1‑cp27‑none‑win_amd64.whl  
```  
  
## <a name="ubuntu-linux"></a>Ubuntu Linux  
  
1. **Installare il runtime di Python e gestione pacchetti pip** Python viene fornito preinstallato in maggior parte delle distribuzioni di Ubuntu.  Se il computer dispone di python installato, è possibile ottenere scaricare il file tarball di origine dal [python.org](https://www.python.org/downloads/) e compilare in locale oppure è possibile usare Gestione pacchetti:  
```  
> sudo apt-get install python   
```  
  
2.  **Apri terminale**  
  
3.  **Installare le dipendenze e modulo pymssql**  
```  
> sudo apt-get --assume-yes update  
> sudo apt-get --assume-yes install freetds-dev freetds-bin  
> sudo apt-get --assume-yes install python-dev python-pip  
> sudo pip install pymssql  
```  
  
## <a name="mac"></a>Mac  
  
1. **Installare il runtime di Python e gestione pacchetti pip**  
A. Passare a [python.org](https://www.python.org/downloads/)  
B. Fare clic sul collegamento appropriato Mac programma di installazione pkg.   
c. Esegui una volta scaricato il pacchetto per installare il runtime di Python  
  
2.  **Apri terminale**  
  
3. **Installare Gestione pacchetti Homebrew**  
```  
> ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"  
```  
  
4.  **Installare FreeTDS modulo**  
```  
> brew install FreeTDS  
```  
  
5.  **Installare pymssql modulo**  
```  
> sudo -H pip install pymssql  
```
