---
title: "Passaggio 1: configurare l'ambiente di sviluppo Python per pyodbc | Microsoft Docs"
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
ms.openlocfilehash: a1a43540d866faaf79b1c020eb255689862e6d97
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67992516"
---
# <a name="step-1-configure-development-environment-for-pyodbc-python-development"></a>Passaggio 1: Configurare l'ambiente di sviluppo per lo sviluppo Python con pyodbc

## <a name="windows"></a>Windows  
Connettersi al database SQL tramite Python-pyodbc in Windows:
  
1. **Scaricare il programma di installazione di Python**.  
  Se il computer non dispone di Python, installarlo. Passare alla [pagina di download di Python](https://www.python.org/downloads/windows/) e scaricare il programma di installazione appropriato. Ad esempio, se si è in un computer a 64 bit, scaricare il programma di installazione di Python 2,7 o 3,7 (x64).  
  
2. **Installare Python**.  Una volta scaricato il programma di installazione, seguire questa procedura: a. Fare doppio clic sul file per avviare il programma di installazione. B. Selezionare la lingua e accettare le condizioni. c. Seguire le istruzioni visualizzate e Python deve essere installato nel computer. d. È possibile verificare che Python `C:\Python27` sia installato selezionando o `C:\Python37` ed eseguendo `python -V` o `py -V` (per 3. x) 
      
3. [**Installare Microsoft ODBC Driver for SQL Server in Windows**](../../odbc/windows/system-requirements-installation-and-driver-files.md#installing-microsoft-odbc-driver-for-sql-server)
  
4. **Aprire cmd. exe come amministratore**     

5. **Installare pyodbc con pip-Python Package Manager** (Sostituire `C:\Python27\Scripts` con il percorso Python installato)
```  
> cd C:\Python27\Scripts  
> pip install pyodbc  
```  

  
## <a name="linux"></a>Linux 
Connettersi al database SQL tramite Python-pyodbc:
  
1. **Apri terminale**  

2. [**Installare Microsoft ODBC Driver for SQL Server in Linux**](../../odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server.md)

3.  **Installare pyodbc**  
```  
> sudo -H pip install pyodbc
```
