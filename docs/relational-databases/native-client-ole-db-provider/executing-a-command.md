---
title: Esecuzione di un comando | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- commands [SQL Server Native Client]
- OLE DB, executing commands
- sessions [SQL Server Native Client]
- OLE DB extensions for XML
- SQL Server Native Client OLE DB provider, command execution
ms.assetid: bb0b3cbf-fe45-46ba-b2ec-c5a39e3c7081
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 88353fa31be9265af5de0e8350aeac5481722351
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290197"
---
# <a name="executing-a-command"></a>Esecuzione di un comando
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Una volta stabilita la connessione a un'origine dati, il consumer chiama il metodo **IDBCreateSession::CreateSession** per creare una sessione. La sessione funge da comando, set di righe o factory di transazioni.  
  
 Per lavorare direttamente con singoli indici o tabelle, il consumer richiede l'interfaccia **IOpenRowset**. Il metodo **IOpenRowset::OpenRowset** apre e restituisce un set di righe che include tutte le righe di un singolo indice o tabella di base.  
  
 Per eseguire un comando, ad esempio SELECT \* FROM Authors, il consumer richiede l'interfaccia **IDBCreateCommand**. Il consumer può eseguire il metodo **IDBCreateCommand::CreateCommand** per creare un oggetto comando e richiedere l'interfaccia **ICommandText**. Il metodo **ICommandText::SetCommandText** viene usato per specificare il comando da eseguire.  
  
 Per eseguire il comando viene usato il comando **Esegui**. Il comando può essere qualsiasi nome di istruzione o di procedura SQL. Non tutti i comandi producono un oggetto set di risultati (set di righe). Comandi come SELECT * FROM Authors producono un set di risultati.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un'applicazione del provider OLE DB di SQL Server Native Client](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
