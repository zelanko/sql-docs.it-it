---
title: Attività File flessibili | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPEXTFILETASK.F1
- SQL14.DTS.DESIGNER.AFPEXTFILETASK.F1
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2d01304a36f7676f53ffef3f6c6e3c600cb87cb6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66411098"
---
# <a name="flexible-file-task"></a>Attività File flessibili

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

L'attività File flessibili consente agli utenti di eseguire operazioni sui file presenti in vari servizi di archiviazione supportati.
I servizi di archiviazione attualmente supportati sono:

- File system locale
- [Archiviazione BLOB di Azure](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)

L'attività File flessibili è un componente del [Feature Pack di SQL Server Integration Services (SSIS) per Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

Per aggiungere un'attività File flessibili a un pacchetto, trascinarla dalla casella degli strumenti SSIS nel canvas di progettazione. Fare quindi doppio clic sull'attività oppure clic con il pulsante destro del mouse sull'attività e selezionare **Modifica** per aprire la finestra di dialogo dell'**editor attività File flessibili**.

La proprietà **Operation** specifica l'operazione file da eseguire.
Al momento è supportata solo l'operazione **Copia**.

Per l'operazione **Copia** sono disponibili le proprietà riportate di seguito.

- **SourceConnectionType:** specifica il tipo di gestione connessione di origine.
- **SourceConnection:** specifica la gestione connessione di origine.
- **SourceFolderPath:** specifica il percorso della cartella di origine.
- **SourceFileName:** specifica il nome file di origine. Se lasciato vuoto, viene copiata la cartella di origine.
- **SearchRecursively:** specifica se le sottocartelle verranno copiate in modo ricorsivo.
- **DestinationConnectionType:** specifica il tipo di gestione connessione di destinazione.
- **DestinationConnection:** specifica la gestione connessione di destinazione.
- **DestinationFolderPath:** specifica il percorso della cartella di destinazione.
- **DestinationFileName:** specifica il nome file di destinazione.
