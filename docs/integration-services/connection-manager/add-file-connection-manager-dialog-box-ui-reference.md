---
title: Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione file | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.fileconnection.f1
helpviewer_keywords:
- Add File Connection Manager
ms.assetid: 9370bfb5-5993-4ad8-a9cd-2de53f320f34
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 226dd6c94787af8c32d17cd7bf923a860645c5ac
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86921715"
---
# <a name="add-file-connection-manager-dialog-box-ui-reference"></a>Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione file

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Utilizzare la finestra di dialogo **Aggiungi gestione connessione file** per definire una connessione a un gruppo di file o cartelle.  
  
 Per ulteriori informazioni sulla gestione connessione per più file, vedere [Multiple Files Connection Manager](../../integration-services/connection-manager/multiple-files-connection-manager.md).  
  
> [!NOTE]  
>  Le attività predefinite e i componenti del flusso di dati in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non utilizzano la gestione connessione per più file. È tuttavia possibile utilizzare la gestione connessione nell'attività Script o nel componente di script.  
  
## <a name="options"></a>Opzioni  
 **Tipo di utilizzo**  
 Consente di specificare il tipo di file da utilizzare per la gestione connessione per più file.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Creazione file**|La gestione connessione creerà i file.|  
|**File esistenti**|La gestione connessione utilizzerà i file esistenti.|  
|**Creazione cartelle**|La gestione connessione creerà le cartelle.|  
|**Cartelle esistenti**|La gestione connessione utilizzerà le cartelle esistenti.|  
  
 **File/Cartelle**  
 Consente di visualizzare i file o le cartelle aggiunti tramite i pulsanti descritti di seguito.  
  
 **Aggiungere**  
 Consente di aggiungere un file usando la finestra di dialogo **Seleziona file** o di aggiungere una cartella usando la finestra di dialogo **Sfoglia cartella** .  
  
 **Modifica**  
 Consente di selezionare un file o una cartella e quindi di sostituirli con un file o una cartella differente usando la finestra di dialogo **Seleziona file** o **Sfoglia cartella** .  
  
 **Rimuovi**  
 Consente di selezionare un file o una cartella e quindi di rimuoverli dall'elenco usando il pulsante **Rimuovi** .  
  
 **Pulsanti freccia**  
 Selezionare un file o una cartella e quindi utilizzare i pulsanti freccia per spostare il file o la cartella verso l'alto o verso il basso in modo da specificare la sequenza di accesso.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../integration-services/integration-services-error-and-message-reference.md)  
  
  
