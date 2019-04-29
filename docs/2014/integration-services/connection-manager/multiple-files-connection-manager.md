---
title: Gestione connessione per più file | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- Multiple Files connection manager
- connection managers [Integration Services], Multiple Files
- connections [Integration Services], files
- multiple file connections
ms.assetid: 10bdc56e-c5cd-4ddb-b2f7-375fe57fe8b2
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 086790cbd654a101d4bced989848d9aaac80d7ad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62833640"
---
# <a name="multiple-files-connection-manager"></a>gestione connessione per più file
  Una gestione connessione per più file consente a un pacchetto di fare riferimento a file e cartelle esistenti o di creare file e cartelle in fase di esecuzione.  
  
> [!NOTE]  
>  Le attività predefinite e i componenti del flusso di dati in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non utilizzano la gestione connessione per più file. È tuttavia possibile utilizzare la gestione connessione nell'attività Script o nel componente di script. Per informazioni sull'uso delle gestioni connessioni nell'attività Script, vedere [Connessione a origini dati nell'attività Script](../extending-packages-scripting/task/connecting-to-data-sources-in-the-script-task.md). Per informazioni sull'utilizzo di gestioni connessioni nel componente Script, vedere [connessione a origini dati nel componente Script] (.. / extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md.  
  
## <a name="usage-types-of-the-multiple-files-connection-manager"></a>Tipi di utilizzo per la gestione connessione per più file  
 La proprietà `FileUsageType` della gestione connessione per più file specifica la modalità di utilizzo della connessione. La gestione connessione per più file consente sia di creare file e cartelle, sia di utilizzare file e cartelle esistenti.  
  
 Nella tabella seguente vengono elencati i possibili valori di `FileUsageType`.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|**0**|La gestione connessione per più file utilizza un file esistente.|  
|**1**|La gestione connessione per più file crea un file.|  
|**2**|La gestione connessione per più file utilizza una cartella esistente.|  
|**3**|La gestione connessione per più file crea una cartella.|  
  
## <a name="configuration-of-the-multiple-files-connection-manager"></a>Configurazione della gestione connessione per più file  
 Quando si aggiunge una gestione connessione per più file a un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione per più file, imposta le proprietà di tale connessione e quindi la aggiunge alla raccolta `Connections` del pacchetto.  
  
 La proprietà `ConnectionManagerType` della gestione connessione viene impostata su `MULTIFILE`.  
  
 Per configurare una gestione connessione per più file, procedere nel modo seguente:  
  
-   Specificare il tipo di utilizzo di file e cartelle.  
  
-   Specificare file e cartelle.  
  
-   Se si utilizzano più file e cartelle, specificare l'ordine con cui accedere a tali elementi.  
  
 Se la gestione connessione per più file fa riferimento a più file e cartelle, i percorsi dei file e delle cartelle sono separati da una barra verticale. La proprietà `ConnectionString` della gestione connessione ha il formato seguente:  
  
 \<*percorso*>|\<*percorso*>  
  
 Per specificare più file o cartelle è inoltre possibile utilizzare caratteri jolly. Ad esempio, fare riferimento a tutti i file di testo in C unità, il valore della `ConnectionString` può essere impostata su c:\\*. txt.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione file](add-file-connection-manager-dialog-box-ui-reference.md).  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  
