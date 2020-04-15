---
title: Voci del Registro di sistema (Driver ODBC di Visual FoxPro) Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304838"
---
# <a name="registry-entries-visual-foxpro-odbc-driver"></a>Voci del Registro di sistema (driver ODBC Visual FoxPro)
Quando si installa il driver ODBC di Visual FoxPro, il programma di installazione aggiorna il Registro di sistema del sistema, nella chiave del Registro di sistema HKEY_LOCAL_MACHINE SOFTWARE, ODBC, ODBCInst.ini, per aggiungere una nuova chiave denominata Driver Microsoft Visual FoxPro. In tale chiave vengono aggiunti i valori descritti nella tabella seguente.  
  
|Nome del valore|Tipo di valore|Valore|  
|----------------|----------------|-----------|  
|Livello API|REG_SZ|"1"|  
|ConnectFunctions (Funzioni di connessione)|REG_SZ|"YYN"|  
|Driver|REG_SZ|Percorso di sistema del file vfpodbc.dll|  
|DriverODBCVer|REG_SZ|"02.50"|  
|FileExtns (Extns)|REG_SZ|".dbf,\*.cdx,\*.fpt"|  
|FileUsage|REG_SZ|"1"|  
|Configurazione|REG_SZ|Percorso di sistema del file vfpodbc.dll|  
|Livello SQL|REG_SZ|"0"|  
  
 Il programma di installazione aggiunge anche la chiave "File Visual FoxPro", che rappresenta il driver Visual FoxPro predefinito, alla chiave HKEY_CURRENT_USER del sistema HKEY_CURRENT_USER SOFTWARE ODBC.ini. In questa chiave, il programma di installazione aggiunge i valori descritti nella tabella seguente.  
  
|Nome del valore|Tipo di valore|Valore|  
|----------------|----------------|-----------|  
|Driver|REG_SZ|Percorso di sistema del file vfpodbc.dll|  
  
 Ogni volta che si aggiunge un'origine dati ODBC Visual FoxPro alla configurazione ODBC, viene aggiunta una nuova chiave per il nome dell'origine dati. I valori per l'origine dati corrispondono ai valori impostati nella finestra di dialogo **Installazione di ODBC Visual FoxPro,** come elencato nella tabella seguente.  
  
|Nome valore (parola chiave)|Tipo di valore|Valore|  
|----------------------------|----------------|-----------|  
|Fascicola|REG_SQ|Qualsiasi sequenza di confronto supportata|  
|Descrizione|REG_SZ|Descrizione utente dell'origine dati|  
|Driver||Percorso di sistema del file vfpodbc.dll|  
|Esclusivo||Sì o No|  
|BackgroundFetch||Sì o No|  
|SourceDB|REG_SZ|Percorso a . File DBC|  
|SourceType|REG_SZ|"DBC" o "DBF"|  
  
 Non è consigliabile accedere direttamente a queste informazioni; qualsiasi amministrazione del Registro di sistema viene gestita dall'Amministratore ODBC quando si aggiunge, modifica o elimina un'origine dati.  
  
 È possibile utilizzare alcune di queste parole chiave e valori come parametri nella funzione API [ODBC SQLDriverConnect.You](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md) can use some of these keywords and values as parameters in the SQLDriverConnect ODBC API function.
