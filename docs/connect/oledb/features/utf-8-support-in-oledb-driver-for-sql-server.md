---
title: Supporto UTF-8 in OLE DB Driver for SQL Server| Microsoft Docs
description: Supporto UTF-8 in OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 04/23/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: v-kaywon
ms.author: v-kaywon
ms.openlocfilehash: d092a534d973de246d3e3c61e67bce9d87d45fe6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "64775175"
---
# <a name="utf-8-support-in-ole-db-driver-for-sql-server"></a>Supporto UTF-8 in OLE DB Driver for SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Microsoft OLE DB Driver for SQL Server (versione 18.2.1) aggiunge il supporto per la codifica server UTF-8. Per informazioni sul supporto della codifica UTF-8 per SQL Server, vedere:
- [Regole di confronto e supporto Unicode](../../../relational-databases/collations/collation-and-unicode-support.md)
- [Supporto UTF-8](#ctp23)

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

<a name="ctp23"></a>

### <a name="utf-8-support-sql-server-2019-ctp-23"></a>Supporto di UTF-8 (SQL Server 2019 CTP 2.3)

In [!INCLUDE[ss2019](../../../includes/sssqlv15-md.md)] viene introdotto il supporto completo per la codifica dei caratteri di grande diffusione UTF-8 come codifica di importazione o esportazione o come regola di confronto di livello database o colonna per i dati di testo. La codifica UTF-8 è consentita nei tipi di dati `CHAR` e `VARCHAR` ed è abilitata quando si crea o si modifica la regola di confronto di un oggetto convertendola in una regola di confronto con il suffisso `UTF8`.

Ad esempio da `LATIN1_GENERAL_100_CI_AS_SC` a `LATIN1_GENERAL_100_CI_AS_SC_UTF8`. UTF-8 è disponibile solo per le regole di confronto di Windows che supportano i caratteri supplementari. Questa funzionalità è stata introdotta in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]. `NCHAR` e `NVARCHAR` consentono solo la codifica UTF-16 e rimangono invariati.

A seconda del set di caratteri in uso, questa funzionalità può offrire importanti risparmi di risorse di archiviazione. Se ad esempio si cambia il tipo di dati di una colonna esistente con stringhe ASCII (Latin) da `NCHAR(10)` in `CHAR(10)` usando una regola di confronto con supporto UTF-8, i requisiti di archiviazione vengono ridotti del 50%. Questa riduzione deriva dal fatto che `NCHAR(10)` richiede 20 byte per l'archiviazione, mentre `CHAR(10)` richiede solo 10 byte per la stessa stringa Unicode.

Per altre informazioni, vedere [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md).

**CTP 2.1** Aggiunge il supporto per la selezione delle regole di confronto UTF-8 come impostazione predefinita durante l'installazione di [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)].

**CTP 2.2** Aggiunge il supporto per l'uso della codifica dei caratteri UTF-8 con la replica di SQL Server.

**CTP 2.3** Aggiunge il supporto per l'uso della codifica dei caratteri UTF-8 con le regole di confronto BIN2 (UTF8_BIN2).

## <a name="see-also"></a>Vedere anche  
[Driver OLE DB per funzionalità di SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md) 

[Supporto UTF-16 nel driver OLE DB per SQL Server](../../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)    
  
  
