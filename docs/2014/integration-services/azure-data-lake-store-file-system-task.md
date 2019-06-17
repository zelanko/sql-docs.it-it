---
title: Attività File system di Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL12.DTS.DESIGNER.AFPADLSTASK.F1
- SQL11.DTS.DESIGNER.AFPADLSTASK.F1
ms.assetid: 02b9edd7-6ef9-463e-abbf-e1830bcae875
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 69a521cb72e68141f5706f5187a0288a3f44f241
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66061383"
---
# <a name="azure-data-lake-store-file-system-task"></a>Attività File system di Azure Data Lake Store

Il **attività di sistema di File di Azure Data Lake Store** consente agli utenti di eseguire varie operazioni del file system sul [Azure Data Lake Store (ADLS)](https://azure.microsoft.com/services/data-lake-store/).

Per aggiungere un'attività File System di Azure Data Lake Store a un pacchetto, trascinarla dalla casella degli strumenti SSIS ai canvas di progettazione. Quindi fare doppio clic su attività, o l'attività e scegliere **modifica**, per aprire la finestra di dialogo Editor dell'attività.

La proprietà **Operation** specifica l'operazione del file system da eseguire. Sono supportate le operazioni seguenti.

* **CopyToADLS:** carica i file in ADLS.
* **CopyFromADLS:** scarica i file da ADLS.

Per qualsiasi operazione è necessario specificare una gestione della connessione di Azure Data Lake.

Di seguito sono riportate le descrizioni delle proprietà specifiche per ogni operazione.

## <a name="copytoadls"></a>CopyToADLS

* **LocalDirectory:** Specifica la directory di origine che contiene i file da caricare.
* **FileNamePattern:** specifica un filtro di nome file per i file di origine. Verranno caricati solo i file il cui nome corrisponde al modello specificato. Sono supportati i caratteri jolly `*` e `?`.
* **SearchRecursively:** specifica se cercare in modo ricorsivo i file da caricare all'interno della directory di origine.
* **AzureDataLakeDirectory:** specifica la directory di destinazione di ADLS in cui caricare i file.
* **FileExpiry:** Specifica una data di scadenza e l'ora per i file caricati in Azure Data Lake Store, o lasciare vuoto per indicare che i file non scadono mai questa proprietà.

## <a name="copyfromadls"></a>CopyFromADLS

* **AzureDataLakeDirectory:** specifica la directory di origine di ADLS che contiene i file da scaricare.
* **SearchRecursively:** specifica se cercare in modo ricorsivo i file da scaricare all'interno della directory di origine.
* **LocalDirectory:** specifica la directory di destinazione in cui archiviare i file scaricati.
