---
title: Esempio di origine dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], examples
ms.assetid: cbf15f32-0550-4c74-8088-8f7ac3855469
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f427074f7cd7153f448aaef43bc4ac5dca84c01
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63186309"
---
# <a name="data-source-example"></a>Esempio di origine dati
Nei computer che eseguono Microsoft® Windows NT® Server o Windows 2000 Server, Microsoft Windows NT Workstation o Windows 2000 Professional o Microsoft Windows® 95 o 98, dati del computer informazioni di origine vengono archiviate nel Registro di sistema. A seconda di quale registro di sistema chiave vengono archiviate le informazioni sotto, l'origine dati è noto come un *origine dati utente* o una *origine dati di sistema*. Le origini dati utente vengono archiviate nella chiave HKEY_CURRENT_USER e sono disponibili solo per l'utente corrente. Origini dati di sistema vengono archiviate nella chiave HKEY_LOCAL_MACHINE e possono essere utilizzate da più di un utente in un computer. Possono inoltre essere utilizzati dai servizi a livello di sistema, che possono quindi ottenere l'accesso all'origine dati anche se nessun utente è connesso al computer. Per altre informazioni sulle origini dati di sistema e utente, vedere [SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md).  
  
 Si supponga che un utente dispone di tre origini di dati utente: Il personale e l'inventario, che usano un DBMS Oracle; e paghe, il che usa un'istanza di Microsoft SQL Server DBMS. I valori del Registro di sistema per le origini dati potrebbero essere:  
  
```  
HKEY_CURRENT_USER  
SOFTWARE  
          ODBC  
               Odbc.ini  
                    ODBC Data Sources  
                    Personnel : REG_SZ : Oracle  
                    Inventory : REG_SZ : Oracle  
                    Payroll : REG_SZ : SQL Server  
```  
  
 e i valori del Registro di sistema per l'origine dati di Payroll potrebbero essere:  
  
```  
HKEY_CURRENT_USER  
     SOFTWARE  
          ODBC  
               Odbc.ini  
                    Payroll  
                         Driver : REG_SZ : C:\WINDOWS\SYSTEM\Sqlsrvr.dll  
                         Description : REG_SZ : Payroll database  
                         Server : REG_SZ : PYRLL1  
                         FastConnectOption : REG_SZ : No                          UseProcForPrepare : REG_SZ : Yes  
                         OEMTOANSI : REG_SZ : No  
                         LastUser : REG_SZ : smithjo  
                         Database : REG_SZ : Payroll  
                         Language : REG_SZ :  
```
