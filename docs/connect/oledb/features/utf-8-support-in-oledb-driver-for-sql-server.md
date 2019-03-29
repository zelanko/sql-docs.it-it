---
title: Supporto UTF-8 in OLE DB Driver for SQL Server| Microsoft Docs
description: Supporto UTF-8 in OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 03/27/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: b7f138438d522c9da1b7ef74acbaf963e17d6144
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492603"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>Supporto UTF-8 in OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Driver Microsoft OLE DB per SQL Server (versione 18.2.1) aggiunge supporto per la codifica UTF-8 server. Per informazioni sul supporto UTF-8 di SQL Server, vedere:
- [Regole di confronto e supporto Unicode](../../../relational-databases/collations/collation-and-unicode-support.md)
- [Supporto UTF-8](../../../sql-server/what-s-new-in-sql-server-ver15.md#utf-8-support-ctp-23)

## <a name="data-insertion-into-a-utf-8-encoded-char-or-varchar-column"></a>Inserimento dei dati in un UTF-8 con codifica colonne CHAR o VARCHAR
Quando si crea un buffer del parametro di input per l'inserimento, il buffer è descritto tramite una matrice di [strutture DBBINDING](https://go.microsoft.com/fwlink/?linkid=2071182). Ogni struttura DBBINDING associa un singolo parametro al buffer del consumer e contiene informazioni quali la lunghezza e tipo del valore di dati. Per un buffer del parametro di input di tipo CHAR, il *wType* di DBBINDING struttura deve essere impostata su DBTYPE_STR. Per un buffer del parametro di input di tipo WCHAR, il *wType* di DBBINDING struttura deve essere impostata su DBTYPE_WSTR.

Quando si esegue un comando con parametri, il driver costruisce informazioni sul tipo di dati di parametro. Se il tipo di buffer di input e dati dei parametri di tipo di corrispondenza, non viene eseguita alcuna conversione nel driver. In caso contrario, il driver converte il buffer del parametro di input per il tipo di dati del parametro. Il tipo di dati del parametro può essere impostato in modo esplicito dall'utente chiamando [ICommandWithParameters:: SetParameterInfo](https://go.microsoft.com/fwlink/?linkid=2071577). Se le informazioni non viene specificate, il driver deriva le informazioni sul tipo di dati del parametro (a) il recupero di metadati della colonna dal server quando viene preparata l'istruzione o (b) tenta una conversione predefinita dal tipo di dati di parametro di input.

Il buffer del parametro di input può essere convertito nelle regole di confronto colonna server tramite il driver o tramite il server a seconda del tipo di dati del buffer di input e il tipo di dati del parametro. Durante la conversione, la perdita di dati può verificarsi se la tabella codici del client o la tabella codici delle regole di confronto del database non può rappresentare tutti i caratteri nel buffer di input. La tabella seguente descrive il processo di conversione durante l'inserimento di dati in un UTF-8 abilitati colonna:

|Tipo di dati del buffer|Tipo di dati del parametro|Conversione|Misura utente|
|---             |---                |---       |---            |
|DBTYPE_STR|DBTYPE_STR|Conversione di server dalla tabella codici del client alla tabella codici delle regole di confronto del database; conversione di server dalla tabella codici delle regole di confronto del database alla tabella codici delle regole di confronto della colonna.|Verificare che la tabella codici del client e la tabella codici delle regole di confronto del database può rappresentare tutti i caratteri nei dati di input. Ad esempio, per inserire un carattere polacco, tabella codici del client può essere impostata su 1250 (ANSI Europa centrale) e le regole di confronto del database è stato possibile polacco come Designazione regole di confronto (ad esempio, Polish_100_CI_AS_SC) oppure deve essere abilitato UTF-8.|
|DBTYPE_STR|DBTYPE_WSTR|Conversione del driver dalla tabella codici del client per la codifica UTF-16; conversione di server dalla codifica UTF-16 alla tabella codici delle regole di confronto della colonna.|Verificare che la tabella codici del client può rappresentare tutti i caratteri nei dati di input. Ad esempio, per inserire un carattere polacco, tabella codici del client potrebbe essere impostare 1250 (ANSI Europa centrale).|
|DBTYPE_WSTR|DBTYPE_STR|Conversione del driver dalla codifica UTF-16 alla tabella codici delle regole di confronto del database; conversione di server dalla tabella codici delle regole di confronto del database alla tabella codici delle regole di confronto della colonna.|Verificare che la tabella codici delle regole di confronto del database può rappresentare tutti i caratteri nei dati di input. Ad esempio, per inserire un carattere polacco, la tabella codici delle regole di confronto del database potrebbe usare polacco come Designazione regole di confronto (ad esempio, Polish_100_CI_AS_SC) oppure essere UTF-8 abilitati.|
|DBTYPE_WSTR|DBTYPE_WSTR|Conversione di server da UTF-16 alla tabella codici delle regole di confronto della colonna.|Nessuna.|

## <a name="data-retrieval-from-a-utf-8-encoded-char-or-varchar-column"></a>Il recupero dei dati da un UTF-8 con codifica colonne CHAR o VARCHAR
Quando si crea un buffer per i dati recuperati, il buffer è descritto tramite una matrice di [strutture DBBINDING](https://go.microsoft.com/fwlink/?linkid=2071182). Ogni struttura DBBINDING associa una singola colonna nella riga recuperata. Per recuperare i dati della colonna di tipo CHAR, impostare il *wType* della struttura DBBINDING in DBTYPE_STR. Per recuperare i dati della colonna come WCHAR, impostare il *wType* della struttura DBBINDING per DBTYPE_WSTR.

Per l'indicatore DBTYPE_STR del tipo di buffer il risultato, il driver converte i dati con codificata UTF-8 al client di codifica. L'utente deve assicurarsi che il client di codifica può rappresentare i dati dalla colonna UTF-8, in caso contrario, potrebbe verificarsi la perdita di dati.

Per l'indicatore DBTYPE_WSTR del tipo di buffer il risultato, il driver converte i dati con codificata UTF-8 per la codifica UTF-16.
  
## <a name="see-also"></a>Vedere anche  
[Driver OLE DB per funzionalità di SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[Supporto UTF-16 nel driver OLE DB per SQL Server](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
