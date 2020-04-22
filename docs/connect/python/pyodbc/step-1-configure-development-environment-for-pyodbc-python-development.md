---
title: "Passaggio 1: Configurare l'ambiente Python con pyodbc"
description: Il passaggio 1 di questa guida introduttiva prevede l'installazione di Python, Microsoft ODBC Driver for SQL Server e pyODBC nell'ambiente di sviluppo.
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1ea669649767f55598190093b7c929f5bd8db27f
ms.sourcegitcommit: 1a96abbf434dfdd467d0a9b722071a1ca1aafe52
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81528515"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>Passaggio 1: Configurare l'ambiente di sviluppo per lo sviluppo Python con pyodbc

## <a name="windows"></a>Windows  
Connettersi al database SQL tramite Python - pyodbc in Windows:
  
1. **Scaricare il programma di installazione di Python**.  
  Se il computer non include Python, installarlo. Passare alla [pagina di download di Python](https://www.python.org/downloads/windows/) e scaricare il programma di installazione appropriato. Se ad esempio si usa un computer a 64 bit, scaricare il programma di installazione di Python 2.7 o 3.7 (x64).  
  
2. **Installare Python**.  Dopo aver scaricato il programma di installazione, seguire questa procedura: a. Fare doppio clic sul file per avviare il programma di installazione. b. Selezionare la lingua e accettare le condizioni. c. Seguire le istruzioni visualizzate e Python verrà installato nel computer. d. Per verificare che Python sia installato passare a `C:\Python27` o `C:\Python37` ed eseguire `python -V` o `py -V` (per 3.x) 
      
3. [**Installare Microsoft ODBC Driver for SQL Server in Windows**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **Aprire cmd.exe come amministratore**     

5. **Installare pyodbc usando la gestione pacchetti pip - Python** (sostituire `C:\Python27\Scripts` con il percorso di installazione di Python)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Connettersi al database SQL tramite Python - pyodbc:
  
1. **Apri terminale**  

2. [**Installare Microsoft ODBC Driver for SQL Server in Linux**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **Installare pyodbc**  
```  
> sudo -H pip install pyodbc
```
