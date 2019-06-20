---
title: Editor gestione connessione file | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fileconnectionmanager.f1
helpviewer_keywords:
- File Connection Manager Editor
ms.assetid: 051c48e5-3d86-49af-b554-ff62e3de3622
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: df54d7fb7562e6019e581b06fd14b00bdba15376
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66058814"
---
# <a name="file-connection-manager-editor"></a>Editor gestione connessione file
  Utilizzare la finestra di dialogo **Editor gestione connessione file** per specificare le proprietà utilizzate per la connessione a un file o a una cartella.  
  
> [!NOTE]  
>  È possibile impostare la proprietà ConnectionString per la gestione connessione file specificando un'espressione nella finestra Proprietà di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Tuttavia, per evitare un errore di convalida quando si usa un'espressione per specificare il file o la cartella, aggiungere il percorso di un file o di una cartella in **Editor gestione connessione file**per **File/Cartella**.  
  
 Per ulteriori informazioni sulla gestione connessione file, vedere [File Connection Manager](connection-manager/file-connection-manager.md).  
  
## <a name="options"></a>Opzioni  
 **Tipo di utilizzo**  
 Consente di specificare se **Gestione connessione file flat** deve connettersi a un file o a una cartella esistente o creare un nuovo file o cartella.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|Creazione file|Consente di creare un nuovo file in fase di esecuzione.|  
|File esistente|Consente di utilizzare un file esistente.|  
|Creazione cartella|Consente di creare una nuova cartella in fase di esecuzione.|  
|Cartella esistente|Consente di utilizzare una cartella esistente.|  
  
 **File/Cartella**  
 Se si sceglie **File**, specificare il file da usare.  
  
 Se si sceglie **Cartella**, specificare la cartella da utilizzare.  
  
 **Sfoglia**  
 Selezionare il file o la cartella usando la finestra di dialogo **Seleziona file** o **Sfoglia cartella** .  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)  
  
  
