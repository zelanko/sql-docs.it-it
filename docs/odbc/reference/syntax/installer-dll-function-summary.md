---
title: Riepilogo delle funzioni della DLL del programma di installazione Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], installer DLL functions
- installer DLL [ODBC]
ms.assetid: 666c09d3-1e10-4d89-9b42-eda2957a87f0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ddaf20334a84833433961a49e17724d354945c5a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298771"
---
# <a name="installer-dll-function-summary"></a>Riepilogo delle funzioni DLL programma di installazione
Nella tabella seguente vengono descritte le funzioni nella DLL del programma di installazione. Per ulteriori informazioni sulla sintassi e la semantica per ogni funzione, vedere [Guida di riferimento all'API DLL del programma](../../../odbc/reference/syntax/installer-dll-api-reference-function.md)di installazione .  
  
|Attività|Nome della funzione|Scopo|  
|----------|-------------------|-------------|  
|Installazione di ODBC|[SQLConfigDriver (driver)](../../../odbc/reference/syntax/sqlconfigdriver-function.md)|Carica la DLL di installazione specifica del driver.|  
||[SQLGetInstalledDrivers (Driver SQLGetInstalledDrivers)](../../../odbc/reference/syntax/sqlgetinstalleddrivers-function.md)|Restituisce un elenco di driver installati.|  
||[SQLInstallDriverEx (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlinstalldriverex-function.md)|Aggiunge un driver alle informazioni di sistema.|  
||[SQLInstallDriverManager (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|Restituisce la directory di destinazione per Gestione Driver.|  
||[Errore SQLInstallerError](../../../odbc/reference/syntax/sqlinstallererror-function.md)|Restituisce informazioni sull'errore o sullo stato per le funzioni del programma di installazione.|  
||[SQLInstallTranslatorEx (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlinstalltranslatorex-function.md)|Aggiunge un traduttore alle informazioni di sistema.|  
||[Errore DI SQLPostInstaller](../../../odbc/reference/syntax/sqlpostinstallererror-function.md)|Consente a un driver o a un traduttore di segnalare gli errori.|  
||[SQLRemoveDriver (sqlRemoveDriver)](../../../odbc/reference/syntax/sqlremovedriver-function.md)|Rimuove un driver dalle informazioni di sistema.|  
||[SQLRemoveDriverManager](../../../odbc/reference/syntax/sqlremovedrivermanager-function.md)|Rimuove i componenti principali ODBC dalle informazioni di sistema.|  
||[SQLRemoveTranslator (TraduttorediSQLRemoveTranslator)](../../../odbc/reference/syntax/sqlremovetranslator-function.md)|Rimuove il traduttore dalle informazioni di sistema.|  
|Configurazione delle origini dati|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|Chiama la DLL di installazione specifica del driver.|  
||[SQLCreateDataSource (origine SQLCreateDataSource)](../../../odbc/reference/syntax/sqlcreatedatasource-function.md)|Visualizza una finestra di dialogo per aggiungere un'origine dati.|  
||[MODALità SQLGetConfigSQLGetConfigMode](../../../odbc/reference/syntax/sqlgetconfigmode-function.md)|Recupera la modalità di configurazione che indica dove si trova la voce Odbc.ini che elenca i valori DSN nelle informazioni di sistema.|  
||[OGGETTO SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|Scrive un valore nelle informazioni di sistema.|  
||[SQLGetTranslator (Traduttore)](../../../odbc/reference/syntax/sqlgettranslator-function.md)|Visualizza una finestra di dialogo per selezionare un traduttore.|  
||[SQLManageDataSources](../../../odbc/reference/syntax/sqlmanagedatasources.md)|Visualizza una finestra di dialogo per configurare le origini dati e i driver.|  
||[SQLReadFileDSN (Informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlreadfiledsn-function.md)|Legge le informazioni dai DSN su file.|  
||[SQLRemoveDefaultDataSource (Origine datiSQLRemoveDefaultDataSource)](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|Rimuove l'origine dati predefinita.|  
||[ISTRUZIONE SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|Rimuove un'origine dati.|  
||[METODO SQLSetConfig](../../../odbc/reference/syntax/sqlsetconfigmode-function.md)|Imposta la modalità di configurazione che indica dove si trova la voce Odbc.ini che elenca i valori DSN nelle informazioni di sistema.|  
||[SQLValidDSN (Istruzione SQLValidDSN)](../../../odbc/reference/syntax/sqlvaliddsn-function.md)|Controlla la lunghezza e la validità del nome dell'origine dati.|  
||[Istruzione SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|Aggiunge un'origine dati.|  
||[SQLWriteFileDSN](../../../odbc/reference/syntax/sqlwritefiledsn-function.md)|Scrive informazioni nei DSN di file.|  
||[OGGETTO SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|Ottiene un valore dalle informazioni di sistema.|
