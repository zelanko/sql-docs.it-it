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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 48c87f0d9f0a48b7d216151178c15bb019c0cbaa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306522"
---
# <a name="data-source-example"></a>Esempio di origine dati
Nei computer in cui è in esecuzione Microsoft® Windows NT® Server/Windows 2000 Server, Microsoft Windows NT Workstation/Windows 2000 Professional o Microsoft Windows® 95/98, le informazioni sull'origine dati del computer vengono archiviate nel registro di sistema. A seconda della chiave del registro di sistema in cui sono archiviate le informazioni, l'origine dati è nota come *origine dati utente* o di *sistema*. Le origini dati utente vengono archiviate con la chiave di HKEY_CURRENT_USER e sono disponibili solo per l'utente corrente. Le origini dati di sistema vengono archiviate sotto la chiave di HKEY_LOCAL_MACHINE e possono essere usate da più di un utente in un computer. Possono anche essere usati dai servizi a livello, che possono quindi ottenere l'accesso all'origine dati anche se nessun utente è connesso al computer. Per ulteriori informazioni sulle origini dati utente e di sistema, vedere [SQLManageDataSources](../../odbc/reference/syntax/sqlmanagedatasources.md).  
  
 Si supponga che un utente disponga di tre origini dati utente: personale e inventario, che utilizzano un sistema DBMS Oracle; e Payroll, che usa un sistema DBMS Microsoft SQL Server. I valori del registro di sistema per le origini dati potrebbero essere:  
  
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
  
 e i valori del registro di sistema per l'origine dati Payroll potrebbero essere:  
  
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
