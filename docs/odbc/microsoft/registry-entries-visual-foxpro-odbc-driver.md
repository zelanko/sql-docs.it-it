---
title: Voci del registro di sistema (driver ODBC Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- registry keys [ODBC]
- Visual FoxPro ODBC driver [ODBC], registry entries
- keys [ODBC]
- FoxPro ODBC driver [ODBC], registry entries
ms.assetid: 1a63d92d-ca3a-46ae-911f-6788292c801e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bd2d419a94c45a872789e095b014159b41d7c217
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304838"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>Voci del Registro di sistema (driver ODBC Visual FoxPro)
Quando si installa il driver ODBC Visual FoxPro, il programma di installazione aggiorna il registro di sistema, nella chiave del registro di sistema HKEY_LOCAL_MACHINE \SOFTWARE\ODBC\ODBCInst.ini, per aggiungere una nuova chiave denominata driver Microsoft Visual FoxPro. Sotto tale chiave vengono aggiunti i valori descritti nella tabella seguente.  
  
|Nome del valore|Tipo di valore|valore|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|Driver|REG_SZ|Percorso di sistema del file Vfpodbc. dll|  
|DriverODBCVer|REG_SZ|"02,50"|  
|FileExtns|REG_SZ|"*. dbf,\*. CDX,\*. FPT"|  
|Fileusage|REG_SZ|"1"|  
|Configurazione|REG_SZ|Percorso di sistema del file Vfpodbc. dll|  
|Sqllevel|REG_SZ|"0"|  
  
 Il programma di installazione aggiunge anche la chiave "Visual FoxPro files", che rappresenta il driver Visual FoxPro predefinito, alla chiave \SOFTWARE\ODBC\Odbc.ini del sistema HKEY_CURRENT_USER. Con questa chiave, il programma di installazione aggiunge i valori descritti nella tabella seguente.  
  
|Nome del valore|Tipo di valore|valore|  
|----------------|----------------|-----------|  
|Driver|REG_SZ|Percorso di sistema del file Vfpodbc. dll|  
  
 Ogni volta che si aggiunge un'origine dati ODBC Visual FoxPro alla configurazione ODBC, viene aggiunta una nuova chiave per il nome dell'origine dati. I valori per l'origine dati corrispondono ai valori impostati nella finestra di dialogo **Configurazione ODBC Visual FoxPro** , come elencato nella tabella seguente.  
  
|Nome valore (parola chiave)|Tipo di valore|valore|  
|----------------------------|----------------|-----------|  
|Fascicola|REG_SQ|Qualsiasi sequenza di confronto supportata|  
|Descrizione|REG_SZ|Descrizione utente dell'origine dati|  
|Driver||Percorso di sistema del file Vfpodbc. dll|  
|Esclusivo||Sì o No|  
|BackgroundFetch||Sì o No|  
|SourceDB|REG_SZ|Percorso di. File DBC|  
|SourceType|REG_SZ|"DBC" o "DBF"|  
  
 Non è consigliabile accedere direttamente a queste informazioni. ogni amministrazione del registro di sistema viene gestita dall'amministratore ODBC quando si aggiunge, modifica o Elimina un'origine dati.  
  
 È possibile utilizzare alcune di queste parole chiave e valori come parametri nella funzione API ODBC [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) .
