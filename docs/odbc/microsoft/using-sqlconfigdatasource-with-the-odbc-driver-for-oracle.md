---
title: Utilizzo di SQLConfigDatasource con il driver ODBC per Oracle . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLConfigDataSource function [ODBC], ODBC driver for Oracle
ms.assetid: e535d1ef-aff9-4ae7-a3ed-ef4ca2584289
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 718e444d63e0d4cf3821c0c03eb851732ed5b4e4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292771"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>Uso di SQLConfigDatasource con il driver ODBC per Oracle
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Nella tabella seguente sono elencate le impostazioni valide di **SQLConfigDatasource** per il driver Microsoft ODBC per Oracle, la versione 1.0 (Msorcl10.dll) e il Driver Microsoft ODBC per Oracle, versione 2.0 (Msorcl32.dll).  
  
> [!NOTE]  
>  Il driver Msorcl10.dll (versione 1.0) supporta tutte le impostazioni ad eccezione **di Server**. Il driver Msorcl32.dll (versione 2.0 e successive) supporta tutte le impostazioni.  
  
 Alcune impostazioni vengono ignorate dal driver, ma vengono accettate da **SQLConfigDatasource**. L'inclusione di queste impostazioni nella stringa di connessione ODBC è l'unico modo in cui verranno accettate in fase di esecuzione. Un'impostazione ignorata non verrà archiviata nel Registro di sistema quando **SQLConfigDatasource** crea l'origine dati.  
  
 Nella tabella seguente, *A/N* indica qualsiasi stringa alfanumerica valida fino alla lunghezza massima consentita. *Intervallo massimo* (lunghezza massima) è la lunghezza massima consentita della stringa accettata dall'impostazione, incluso il carattere di terminazione della stringa.  
  
|Impostazione|Max Len|Valore predefinito|Valori validi|Descrizione|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|Dimensione minima del buffer di recupero fino a 65535 byte|  
|CatalogCap|2|1|0 o 1|Se 1, gli identificatori senza virgolette verranno convertiti in lettere maiuscole nelle funzioni di catalogo.|  
|Stringa di connessioneConnectString|128|""|A/N|Stringa di connessione. Metodo obbligatorio per specificare il nome del server con il driver Msorcl10.dll.|  
|Descrizione|256|""|A/N|Descrizione|  
|DSN|33|""|A/N|Nome dell'origine dati.|  
|GuessTheColDef|4|0|A/N|Restituisce un valore diverso da zero per le colonne senza scala definita da Oracle.|  
|NumeroFloat|2|""|0 o 1|Se 0, le colonne FLOAT vengono considerate come SQL_FLOAT. Se 1, le colonne FLOAT vengono considerate come SQL_DOUBLE.|  
|PWD|30|""|A/N|Password.|  
|Supporto RDOSupport|2|""|0 o 1|Consente a RDO di chiamare le routine Oracle.|  
|Osservazioni|2|0|0 o 1|Includere OSSERVAZIONI nelle funzioni di catalogo.|  
|Limite di rigaRowLimit|4|""|Da 0 a 99 anni|Numero massimo di righe restituite da un'istruzione SELECT. Una stringa di lunghezza zero indica che non viene applicato alcun limite.|  
|Server|128|""|A/N|Nome del server Oracle.|  
|Colonne sinonimi|2|1|0 o 1|Includere SYNONYMs in SQLColumns.|  
|Tabella sistema|2|""|0 o 1|Se 0, le tabelle di sistema non verranno visualizzate. Se 1, verranno visualizzate le tabelle di sistema.|  
|Dll di traduzione|33|""|A/N|Nome .dll di traduzione.|  
|NomeTraduzione|33|""|A/N|Nome della traduzione.|  
|TranslationOption (Opzione)TranslationOption (|33|""|A/N|Opzione di traduzione.|  
|TxnCap|2|""|A/N|Transazione in grado. Se 0, il driver segnala che non supporta le transazioni. Se 1, il driver segnala che è in grado di eseguire le transazioni.|  
|UID|30|""|A/N|Nome utente.|
