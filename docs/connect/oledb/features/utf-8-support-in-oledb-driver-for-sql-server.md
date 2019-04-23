---
title: Supporto UTF-8 in OLE DB Driver for SQL Server| Microsoft Docs
description: Supporto UTF-8 in OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 03/27/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: 4a30b233190817faee581106db5c8a18695a00d1
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59583014"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>Supporto UTF-8 in OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Microsoft OLE DB Driver for SQL Server (versione 18.2.1) aggiunge il supporto per la codifica server UTF-8. Per informazioni sul supporto della codifica UTF-8 per SQL Server, vedere:
- [Regole di confronto e supporto Unicode](../../../relational-databases/collations/collation-and-unicode-support.md)
- [Supporto UTF-8](../../../sql-server/what-s-new-in-sql-server-ver15.md#utf-8-support-ctp-23)

## <a name="data-insertion-into-a-utf-8-encoded-char-or-varchar-column"></a>Inserimento dei dati in una colonna CHAR or VARCHAR con codifica UTF-8
Quando si crea un buffer del parametro di input per l'inserimento, il buffer viene descritto tramite una matrice di [strutture DBBINDING](https://go.microsoft.com/fwlink/?linkid=2071182). Ogni struttura DBBINDING associa un singolo parametro al buffer del consumer e contiene informazioni come la lunghezza e il tipo del valore dati. Per un buffer del parametro di input di tipo CHAR, il campo *wType* della struttura DBBINDING deve essere impostato su DBTYPE_STR. Per un buffer del parametro di input di tipo WCHAR, il campo *wType* della struttura DBBINDING deve essere impostato su DBTYPE_WSTR.

Quando si esegue un comando con i parametri, il driver costruisce informazioni sul tipo di dati dei parametri. Se il tipo di buffer di input e il tipo di dati del parametro corrispondono, non viene eseguita alcuna conversione nel driver. In caso contrario, il driver converte il buffer del parametro di input nel tipo di dati del parametro. Il tipo di dati del parametro può essere impostato in modo esplicito dall'utente chiamando [ICommandWithParameters::SetParameterInfo](https://go.microsoft.com/fwlink/?linkid=2071577). Se le informazioni non vengono specificate, il driver deriva le informazioni sul tipo di dati del parametro (a) recuperando i metadati della colonna dal server quando viene preparata l'istruzione o (b) tentando una conversione predefinita dal tipo di dati del parametro di input.

Il buffer del parametro di input può essere convertito nelle regole di confronto della colonna server dal driver o dal server a seconda del tipo di dati del buffer di input e del tipo di dati del parametro. Durante la conversione, può verificarsi la perdita dei dati se la tabella codici del client o la tabella codici delle regole di confronto del database non è in grado di rappresentare tutti i caratteri nel buffer di input. La tabella seguente descrive il processo di conversione durante l'inserimento dei dati nella colonna che supporta UTF-8:

|Tipo di dati del buffer|Tipo di dati del parametro|Conversione|Precauzione per l'utente|
|---             |---                |---       |---            |
|DBTYPE_STR|DBTYPE_STR|Conversione server dalla tabella codici del client alla tabella codici delle regole di confronto del database; conversione server dalla tabella codici delle regole di confronto del database alla tabella codici delle regole di confronto della colonna.|Verificare che la tabella codici del client e la tabella codici delle regole di confronto del database siano in grado di rappresentare tutti i caratteri nei dati di input. Per inserire un carattere polacco, la tabella codici del client può ad esempio essere impostata su 1250 (ANSI dell'Europa centrale) e le regole di confronto del database possono avvalersi del polacco come designazione delle regole di confronto (ad esempio Polish_100_CI_AS_SC) oppure supportare UTF-8.|
|DBTYPE_STR|DBTYPE_WSTR|Conversione driver dalla tabella codici del client alla codifica UTF-16; conversione server dalla codifica UTF-16 alla tabella codici delle regole di confronto della colonna.|Verificare che la tabella codici del client sia in grado di rappresentare tutti i caratteri nei dati di input. Per inserire un carattere polacco, la tabella codici del client potrebbe ad esempio essere impostata su 1250 (ANSI dell'Europa centrale).|
|DBTYPE_WSTR|DBTYPE_STR|Conversione driver dalla codifica UTF-16 alla tabella codici delle regole di confronto del database; conversione server dalla tabella codici delle regole di confronto del database alla tabella codici delle regole di confronto della colonna.|Verificare che la tabella codici delle regole di confronto del database sia in grado di rappresentare tutti i caratteri nei dati di input. Per inserire un carattere polacco, la tabella codici delle regole di confronto del database può ad esempio avvalersi del polacco come designazione delle regole di confronto (ad esempio Polish_100_CI_AS_SC) oppure supportare UTF-8.|
|DBTYPE_WSTR|DBTYPE_WSTR|Conversione server da UTF-16 alla tabella codici delle regole di confronto della colonna.|Nessuna.|

## <a name="data-retrieval-from-a-utf-8-encoded-char-or-varchar-column"></a>Recupero dati da una colonna CHAR or VARCHAR con codifica UTF-8
Quando si crea un buffer per i dati recuperati, il buffer viene descritto tramite una matrice di [strutture DBBINDING](https://go.microsoft.com/fwlink/?linkid=2071182). Ogni struttura DBBINDING associa una singola colonna nella riga recuperata. Per recuperare i dati della colonna di tipo CHAR, impostare il campo *wType* della struttura DBBINDING su DBTYPE_STR. Per recuperare i dati della colonna di tipo WCHAR, impostare il campo *wType* della struttura DBBINDING su DBTYPE_WSTR.

Per l'indicatore del tipo di buffer DBTYPE_STR, il driver converte i dati con codifica UTF-8 nella codifica del client. L'utente deve assicurarsi che la codifica client sia in grado di rappresentare i dati della colonna UTF-8. In caso contrario potrebbe verificarsi la perdita dei dati.

Per l'indicatore del tipo di buffer DBTYPE_WSTR, il driver converte i dati con codifica UTF-8 nella codifica UTF-16.
  
## <a name="see-also"></a>Vedere anche  
[Driver OLE DB per funzionalità di SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[Supporto UTF-16 nel driver OLE DB per SQL Server](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
