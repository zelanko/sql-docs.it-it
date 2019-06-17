---
title: "Passaggio 1: Configurare l'ambiente di sviluppo Python pyodbc | Microsoft Docs"
ms.custom: ''
ms.date: 07/06/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 74e69704-e63c-450b-9207-5c1491d0e0f5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 549118445c3aaac0f08328074dad412d8c257a49
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66780427"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>Passaggio 1: Configurare l'ambiente di sviluppo per lo sviluppo Python con pyodbc

## <a name="windows"></a>Windows  
Connettersi al Database SQL tramite Python - pyodbc su Windows:
  
1. **Scarica programma di installazione di Python**.  
  Se il computer dispone di Python, è necessario installarlo. Andare alla [pagina di download di Python](https://www.python.org/downloads/windows/) e scaricare il programma di installazione appropriato. Ad esempio, se si usa un computer a 64 bit, scaricare il programma di installazione di Python 2.7 o 3.7 (x64).  
  
2. **Installare Python**.  Dopo aver scaricato il programma di installazione, procedere come segue: una. Fare doppio clic sul file per avviare il programma di installazione. B. Selezionare la lingua e accettare le condizioni. c. Seguire le istruzioni sullo schermo e Python devono essere installati nel computer. d. È possibile verificare che Python è installato, passare a `C:\Python27` oppure `C:\Python37` ed eseguire `python -V` o `py -V` (per 3.x) 
      
3. [**Installare Microsoft ODBC Driver for SQL Server in Windows**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **Aprire cmd.exe come amministratore**     

5. **Installare pyodbc tramite pip - Gestione pacchetti Python** (Sostituisci `C:\Python27\Scripts` con il percorso di Python installato)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Connettersi al Database SQL tramite Python - pyodbc:
  
1. **Apri terminale**  

2. [**Installare Microsoft ODBC Driver for SQL Server in Linux**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **Installare pyodbc**  
```  
> sudo -H pip install pyodbc
```
