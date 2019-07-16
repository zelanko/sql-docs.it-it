---
title: Le voci del Registro di sistema (Driver ODBC Visual FoxPro) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 00a24ffca764c029b87470b7aa07d15f33b4c673
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67996446"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>Voci del Registro di sistema (driver ODBC Visual FoxPro)
Quando si installa il Driver ODBC Visual FoxPro, il programma di installazione aggiorna il Registro di sistema nella chiave del Registro di sistema HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCInst.ini, aggiungere una nuova chiave denominata driver per Microsoft Visual FoxPro. Con la chiave, vengono aggiunti valori descritti nella tabella seguente.  
  
|Nome del valore|Tipo valore|Value|  
|----------------|----------------|-----------|  
|APILevel|REG_SZ|"1"|  
|ConnectFunctions|REG_SZ|"YYN"|  
|Driver|REG_SZ|Percorso di sistema per il file vfpodbc|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns|REG_SZ|"*.dbf,\*.cdx,\*.fpt"|  
|FileUsage|REG_SZ|"1"|  
|Configurazione|REG_SZ|Percorso di sistema per il file vfpodbc|  
|SQLLevel|REG_SZ|"0"|  
  
 Il programma di installazione aggiunge anche la chiave "Visual FoxPro Files", che rappresenta il driver di Visual FoxPro predefinite, alla chiave HKEY_CURRENT_USER\SOFTWARE\ODBC\Odbc.ini del sistema. In questa chiave, il programma di installazione aggiunge i valori descritti nella tabella seguente.  
  
|Nome del valore|Tipo valore|Value|  
|----------------|----------------|-----------|  
|Driver|REG_SZ|Percorso di sistema per il file vfpodbc|  
  
 Ogni volta che si aggiunge un'origine dati ODBC Visual FoxPro alla configurazione ODBC, viene aggiunta una nuova chiave per tale nome dell'origine dati. I valori per l'origine dati corrispondono ai valori impostati nel **programma di installazione di ODBC Visual FoxPro** finestra di dialogo, come indicato nella tabella seguente.  
  
|Nome del valore (parola chiave)|Tipo valore|Value|  
|----------------------------|----------------|-----------|  
|Fascicola|REG_SQ|Qualsiasi sequenza di confronto è supportata|  
|Descrizione|REG_SZ|Descrizione dell'origine dati utente|  
|Driver||Percorso di sistema per il file vfpodbc|  
|Exclusive||Sì o No|  
|BackgroundFetch||Sì o No|  
|SourceDB|REG_SZ|Percorso. File a due byte|  
|SourceType|REG_SZ|"DBC" o "DBF"|  
  
 Non è necessario accedere direttamente; queste informazioni qualsiasi amministrazione del Registro di sistema viene gestito dall'amministratore ODBC quando si aggiungere, modificare o eliminare un'origine dati.  
  
 È possibile usare alcune di queste parole chiave e i valori dei parametri in di [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) funzione API ODBC.
