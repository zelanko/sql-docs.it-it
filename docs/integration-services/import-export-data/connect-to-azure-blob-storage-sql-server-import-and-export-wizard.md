---
title: Connettersi all'archiviazione BLOB di Azure (Importazione/Esportazione guidata SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: e2e482b8-5f90-48c5-93fb-b412ed52659f
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b578b024392edf8c2a8bc2363b8a824bce502555
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68114535"
---
# <a name="connect-to-azure-blob-storage-sql-server-import-and-export-wizard"></a>Connettersi all'archiviazione BLOB di Azure (Importazione/Esportazione guidata SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


Questo argomento illustra come connettersi a un'origine dati **Archiviazione BLOB di Azure** dalla pagina **Scelta origine dati** o **Scelta destinazione** dell'Importazione/Esportazione guidata SQL Server.

> [!NOTE]
> Per usare l'origine o la destinazione BLOB di Azure, è necessario installare il Feature Pack di Azure per SQL Server Integration Services.
> - Per scaricare il Feature Pack, vedere [Microsoft SQL Server 2016 Integration Services Feature Pack per Azure](https://www.microsoft.com/download/details.aspx?id=49492).
> 
> - Per altre informazioni, vedere [Azure Feature Pack for Integration Services &#40;SSIS&#41;](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Lo screenshot seguente mostra le opzioni da configurare per una connessione all'archiviazione BLOB di Azure.

![Connessione all'archiviazione BLOB di Azure](../../integration-services/import-export-data/media/azure-blob-storage-connection.png)

## <a name="options-to-specify"></a>Opzioni da specificare

> [!NOTE]
> Le opzioni di connessione per il provider di dati sono le stesse sia nel caso in cui l'archiviazione BLOB di Azure rappresenti l'origine sia nel caso in cui rappresenti la destinazione. Ovvero, le opzioni visualizzate sono le stesse in entrambe le pagine **Scelta origine dati** e **Scelta destinazione** della procedura guidata.

 **Usa account Azure**  
 Consente di specificare se usare un account online.
  
 **Nome dell'account di archiviazione**  
 Immettere il nome dell'account di archiviazione di Azure.  
  
**Chiave dell'account**  
Immettere la chiave dell'account di archiviazione di Azure.  
  
 **Usa HTTPS**  
 Specificare se usare HTTP o HTTPS per connettersi all'account di archiviazione.  
  
 **Usa account per sviluppatore locale**  
 Specificare se usare l'emulatore di archiviazione nel computer locale.  
  
 **Nome del contenitore BLOB**  
 Selezionare dall'elenco dei contenitori di archiviazione disponibili nell'account di archiviazione specificato.  
  
 **Formato del file BLOB**  
 Selezionare il formato di file Testo o Avro.  
  
 **Carattere delimitatore di colonna**  
 Se è stato selezionato il formato Testo, immettere il carattere delimitatore di colonna.  
  
 **Usa la prima riga come nomi di colonna**  
 Specificare se la prima riga di dati contiene nomi di colonna.  

## <a name="see-also"></a>Vedere anche
[Scelta origine dati](../../integration-services/import-export-data/choose-a-data-source-sql-server-import-and-export-wizard.md)  
[Scelta destinazione](../../integration-services/import-export-data/choose-a-destination-sql-server-import-and-export-wizard.md)

