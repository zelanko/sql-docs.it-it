---
title: Attività di caricamento BLOB di Azure | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.afpblobuptask.f1
- sql11.dts.designer.afpblobuptask.f1
ms.assetid: 6ea068b0-4cd8-45b5-b89d-09b8f25040c0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 392fcbf3a46b48b2032b5792321e9a22b3027341
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62832782"
---
# <a name="azure-blob-upload-task"></a>Attività di caricamento BLOB di Azure
  L'attività di caricamento BLOB di Azure consente a un pacchetto di SSIS di caricare file in un archivio BLOB di Azure.   
Per aggiungere un' **attività di caricamento BLOB di Azure**, trascinare l'attività in Progettazione SSIS e fare doppio clic oppure clic con il pulsante destro del mouse e quindi scegliere **Modifica** per visualizzare la finestra di dialogo seguente relativa all' **editor dell'attività di caricamento BLOB di Azure** .  
  
 La tabella seguente fornisce le descrizioni dei campi della finestra di dialogo.  
  
|||  
|-|-|  
|**Campo**|**Descrizione**|  
|AzureStorageConnection|Consente di specificare un'istanza esistente di Gestione connessioni dell'archiviazione di Azure o di creare una nuova istanza che fa riferimento a un account di archiviazione di Azure che indica la posizione in cui sono ospitati i file BLOB.|  
|BlobContainer|Specifica il nome del contenitore BLOB che conterrà i file caricati come BLOB.|  
|BlobDirectory|Specifica la directory BLOB in cui verrà archiviato il file caricato come BLOB in blocchi. La directory BLOB è una struttura gerarchica virtuale. Se il BLOB esiste già, verrà sostituito.|  
|LocalDirectory|Specifica il nome della directory locale che contiene i file da caricare.|  
|FileName|Specifica un filtro per i nomi per la selezione di file con il modello di nomi specificato. ad esempio MySheet*.xls\* include file quali MySheet001.xls e MySheetABC.xlsx.|  
|TimeRangeFrom/TimeRangeTo|Specifica un filtro basato su un intervallo di tempo. Saranno inclusi i file modificati dopo **TimeRangeFrom** e prima di **TimeRangeTo** .|  
  
  
