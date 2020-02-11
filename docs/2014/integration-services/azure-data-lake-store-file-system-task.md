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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66061383"
---
# <a name="azure-data-lake-store-file-system-task"></a>Attività File system di Azure Data Lake Store

L' **attività Azure Data Lake Store file System** consente agli utenti di eseguire varie operazioni di file system su [Azure Data Lake Store (ADLS)](https://azure.microsoft.com/services/data-lake-store/).

Per aggiungere un'attività File System di Azure Data Lake Store a un pacchetto, trascinarla dalla casella degli strumenti SSIS ai canvas di progettazione. Fare quindi doppio clic sull'attività o fare clic con il pulsante destro del mouse sull'attività e scegliere **modifica**per aprire la finestra di dialogo Editor attività.

La proprietà **Operation** specifica l'operazione del file system da eseguire. Le operazioni supportate sono elencate di seguito.

* **CopyToADLS** per caricare file in ADLS.
* **CopyFromADLS** per scaricare file da ADLS.

Per qualsiasi operazione è necessario specificare una gestione della connessione di Azure Data Lake.

Di seguito sono riportate le descrizioni delle proprietà specifiche per ogni operazione.

## <a name="copytoadls"></a>CopyToADLS

* **LocalDirectory:** Specifica la directory di origine che contiene i file da caricare.
* **FileNamePattern:** specifica un filtro di nome file per i file di origine. Verranno caricati solo i file il cui nome corrisponde al modello specificato. Sono supportati i caratteri jolly `*` e `?`.
* **SearchRecursively:** specifica se cercare in modo ricorsivo i file da caricare all'interno della directory di origine.
* **AzureDataLakeDirectory:** specifica la directory di destinazione di ADLS in cui caricare i file.
* **Fileexpire:** Specifica una data e un'ora di scadenza per i file caricati in ADLS o lasciare vuota questa proprietà per indicare che i file non scadono mai.

## <a name="copyfromadls"></a>CopyFromADLS

* **AzureDataLakeDirectory:** specifica la directory di origine di ADLS che contiene i file da scaricare.
* **SearchRecursively:** specifica se cercare in modo ricorsivo i file da scaricare all'interno della directory di origine.
* **LocalDirectory:** specifica la directory di destinazione in cui archiviare i file scaricati.
