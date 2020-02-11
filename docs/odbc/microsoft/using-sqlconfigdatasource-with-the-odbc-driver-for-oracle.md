---
title: Utilizzo di SQLConfigDatasource con il driver ODBC per Oracle | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa5f1ecf9f3100480081e3744fc7d280a4da282b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088027"
---
# <a name="using-sqlconfigdatasource-with-the-odbc-driver-for-oracle"></a>Uso di SQLConfigDatasource con il driver ODBC per Oracle
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di usare questa funzionalità in un nuovo progetto di sviluppo e prevedere interventi di modifica nelle applicazioni in cui è attualmente implementata. Utilizzare invece il driver ODBC fornito da Oracle.  
  
 Nella tabella seguente sono elencate le impostazioni **SQLConfigDataSource** valide per Microsoft ODBC driver for Oracle, versione 1,0 (Msorcl10. dll) e Microsoft ODBC driver for Oracle, versione 2,0 (Msorcl32. dll).  
  
> [!NOTE]  
>  Il driver Msorcl10. dll (versione 1,0) supporta tutte le impostazioni eccetto **Server**. Il driver msorcl32. dll (versione 2,0 e successive) supporta tutte le impostazioni.  
  
 Alcune impostazioni vengono ignorate dal driver ma sono accettate da **SQLConfigDataSource**. L'inclusione di queste impostazioni nella stringa di connessione ODBC è l'unico modo in cui verranno accettate in fase di esecuzione. Un'impostazione ignorata non verrà archiviata nel registro di sistema quando **SQLConfigDataSource** crea l'origine dati.  
  
 Nella tabella seguente, *a/N* indica qualsiasi stringa alfanumerica valida fino alla lunghezza massima consentita. *Max Len* (lunghezza massima) è la lunghezza massima consentita per la stringa accettata dall'impostazione, incluso il carattere di terminazione della stringa.  
  
|Impostazione|Lunghezza massima|Valore predefinito|Valori validi|Descrizione|  
|-------------|-------------|-------------------|------------------|-----------------|  
|BufferSize|7|65535|1000|Dimensioni minime del buffer di recupero fino a 65535 byte|  
|CatalogCap|2|1|0 o 1|Se è 1, gli identificatori non delimitati verranno convertiti in caratteri maiuscoli nelle funzioni di catalogo.|  
|ConnectString|128|""|A/N|Stringa di connessione. Metodo obbligatorio per specificare il nome del server con il driver Msorcl10. dll.|  
|Descrizione|256|""|A/N|Descrizione|  
|DSN|33|""|A/N|Nome dell'origine dati.|  
|GuessTheColDef|4|0|A/N|Restituisce un valore diverso da zero per le colonne senza scala definita da Oracle.|  
|NumberFloat|2|""|0 o 1|Se è 0, le colonne FLOAT vengono considerate come SQL_FLOAT. Se il valore è 1, le colonne FLOAT vengono considerate come SQL_DOUBLE.|  
|PWD|30|""|A/N|Password.|  
|RDOSupport|2|""|0 o 1|Consente a RDO di chiamare le procedure Oracle.|  
|Osservazioni|2|0|0 o 1|Includere osservazioni nelle funzioni di catalogo.|  
|RowLimit|4|""|da 0 a 99|Numero massimo di righe restituite da un'istruzione SELECT. Una stringa di lunghezza zero indica che non viene applicato alcun limite.|  
|Server|128|""|A/N|Nome del server Oracle.|  
|SynonymColumns|2|1|0 o 1|Includere sinonimi in SQLColumns.|  
|SystemTable|2|""|0 o 1|Se è 0, le tabelle di sistema non verranno visualizzate. Se è 1, verranno visualizzate le tabelle di sistema.|  
|TranslationDLL|33|""|A/N|Nome della traduzione. dll.|  
|Translationname|33|""|A/N|Nome della traduzione.|  
|TranslationOption|33|""|A/N|Opzione di conversione.|  
|TxnCap|2|""|A/N|Transazione in grado di supportare. Se è 0, il driver segnala che non supporta le transazioni. Se è 1, il driver segnala che è in grado di eseguire transazioni.|  
|UID|30|""|A/N|Nome utente.|
