---
title: Gestione connessione file | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.fileconnectionmanager.f1
helpviewer_keywords:
- folders [Integration Services], connections
- files [Integration Services], connections
- files [Integration Services]
- connection managers [Integration Services], File
- connections [Integration Services], files
- File connection manager
ms.assetid: 019078bc-44ee-4975-9169-0f9a89e3f3be
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6c2578e1f002878ade93551a5abc48dfd2144709
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294511"
---
# <a name="file-connection-manager"></a>gestione connessione file

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Una gestione connessione file consente a un pacchetto di fare riferimento a un file o a una cartella esistente oppure di creare un file o una cartella in fase di esecuzione. Ad esempio, è possibile fare riferimento a un file di Excel. Le informazioni presenti nei file vengono utilizzate da alcuni componenti di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per effettuare le operazioni. L'attività Esegui SQL può ad esempio fare riferimento a un file che contiene le istruzioni SQL eseguite dall'attività. In altri componenti le operazioni vengono effettuate nei file. Ad esempio, tramite l'attività File System è possibile fare riferimento a un file per copiarlo in una nuova posizione.  
  
## <a name="usage-types-of-the-file-connection-manager"></a>Tipi di utilizzo per la gestione connessione file  
 Tramite la proprietà **FileUsageType** della gestione connessione file viene specificata la modalità di utilizzo della connessione file. La gestione connessione file può creare un file o una cartella oppure utilizzare un file o una cartella esistente.  
  
 Nella tabella seguente vengono elencati i possibili valori di **FileUsageType**.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**0**|La gestione connessione file utilizza un file esistente.|  
|**1**|La gestione connessione file crea un file.|  
|**2**|La gestione connessione file utilizza una cartella esistente.|  
|**3**|La gestione connessione file crea una cartella.|  
  
## <a name="multiple-file-or-folder-connections"></a>Connessioni a più file o cartelle  
 La gestione connessione file può fare riferimento solo a un file o a una cartella. Per fare riferimento a più file o cartelle, al posto di una gestione connessione file utilizzare una gestione connessione per più file. Per altre informazioni, vedere [Multiple Files Connection Manager](../../integration-services/connection-manager/multiple-files-connection-manager.md).  
  
## <a name="configuration-of-the-file-connection-manager"></a>Configurazione della gestione connessione file  
 Quando si aggiunge una gestione connessione file a un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione file, imposta le proprietà della connessione file e la aggiunge alla raccolta **Connections** del pacchetto.  
  
 La proprietà **ConnectionManagerType** della gestione connessione viene impostata su **FILE**.  
  
 Per configurare una gestione connessione file, procedere nel modo seguente:  
  
-   Specificare il tipo di utilizzo.  
  
-   Specificare un file o una cartella.  
  
 È possibile impostare la proprietà ConnectionString per la gestione connessione file specificando un'espressione nella finestra Proprietà di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Tuttavia, per evitare un errore di convalida quando si usa un'espressione per specificare il file o la cartella, aggiungere il percorso di un file o di una cartella in **Editor gestione connessione file**per **File/Cartella**.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Editor gestione connessione file](../../integration-services/connection-manager/file-connection-manager-editor.md).  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="file-connection-manager-editor"></a>Editor gestione connessione file
  Utilizzare la finestra di dialogo **Editor gestione connessione file** per specificare le proprietà utilizzate per la connessione a un file o a una cartella.  
  
> [!NOTE]  
>  È possibile impostare la proprietà ConnectionString per la gestione connessione file specificando un'espressione nella finestra Proprietà di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Tuttavia, per evitare un errore di convalida quando si usa un'espressione per specificare il file o la cartella, aggiungere il percorso di un file o di una cartella in **Editor gestione connessione file**per **File/Cartella**.  
  
 Per ulteriori informazioni sulla gestione connessione file, vedere [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
### <a name="options"></a>Opzioni  
 **Tipo di utilizzo**  
 Consente di specificare se **Gestione connessione file flat** deve connettersi a un file o a una cartella esistente o creare un nuovo file o cartella.  
  
|valore|Descrizione|  
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
  
  
