---
title: Attività File system di Azure Data Lake Store | Microsoft Docs
ms.custom: ''
ms.date: 08/22/2017
ms.prod: sql
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- SQL13.DTS.DESIGNER.AFPADLSTASK.F1
- SQL14.DTS.DESIGNER.AFPADLSTASK.F1
author: Lingxi-Li
ms.author: lingxl
ms.reviewer: maghan
ms.openlocfilehash: 9460730ae4756bb2862de751bc72cad649e38298
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913887"
---
# <a name="azure-data-lake-store-file-system-task"></a>Attività File system di Azure Data Lake Store

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]



L'attività File System di Azure Data Lake Store consente agli utenti di eseguire varie operazioni del file system in [Azure Data Lake Store (ADLS)](https://azure.microsoft.com/services/data-lake-store/).

L'attività File System di Azure Data Lake Store è un componente del [Feature Pack di SQL Server Integration Services (SSIS) per Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).

## <a name="configure-the-azure-data-lake-store-file-system-task"></a>Configurare l'attività File system di Azure Data Lake Store

Per aggiungere un'attività File System di Azure Data Lake Store a un pacchetto, trascinarla dalla casella degli strumenti SSIS ai canvas di progettazione. Fare doppio clic sull'attività o fare clic con il pulsante destro del mouse e selezionare **Modifica** per aprire la finestra di dialogo dell'**editor dell'attività File system Azure Data Lake Store**.

La proprietà **Operation** specifica l'operazione del file system da eseguire. Selezionare una delle operazioni seguenti:

- **CopyToADLS** per caricare file in ADLS.
- **CopyFromADLS** per scaricare file da ADLS.

## <a name="configure-the-properties-for-the-operation"></a>Configurare le proprietà per l'operazione
Per qualsiasi operazione è necessario specificare una gestione della connessione di Azure Data Lake.

Di seguito sono riportate le proprietà specifiche per ogni operazione:

### <a name="copytoadls"></a>CopyToADLS
- **LocalDirectory:** specifica la directory di origine locale che contiene i file da caricare.
- **FileNamePattern:** specifica un filtro di nome file per i file di origine. Vengono caricati solo i file i cui nomi corrispondono al modello specificato. Sono supportati i caratteri jolly `*` e `?`.
- **SearchRecursively:** specifica se cercare in modo ricorsivo i file da caricare all'interno della directory di origine.
- **AzureDataLakeDirectory:** specifica la directory di destinazione di ADLS in cui caricare i file.
- **FileExpiry:** specifica una data e un'ora di scadenza per i file caricati in ADLS. Lasciare questa proprietà vuota per indicare che i file non scadono mai.

### <a name="copyfromadls"></a>CopyFromADLS
- **AzureDataLakeDirectory:** specifica la directory di origine di ADLS che contiene i file da scaricare.
- **SearchRecursively:** specifica se cercare in modo ricorsivo i file da scaricare all'interno della directory di origine.
- **LocalDirectory:** specifica la directory di destinazione in cui archiviare i file scaricati.
