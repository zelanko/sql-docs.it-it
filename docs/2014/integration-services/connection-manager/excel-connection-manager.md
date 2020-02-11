---
title: Gestione connessione Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 432d48bbe848d6f66e9f3dae5365abe10d8deb62
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833845"
---
# <a name="excel-connection-manager"></a>Gestione connessione Excel
  Una gestione connessione Excel consente la connessione di un pacchetto a un file di cartella di lavoro di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel esistente. L'origine Excel e la destinazione Excel che [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] includono utilizzano la gestione connessione Excel.  
  
 Quando si aggiunge una gestione connessione Excel a un pacchetto, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione verrà risolta in una connessione Excel, imposta le proprietà della gestione connessione e quindi la aggiunge alla raccolta `Connections` del pacchetto.  
  
 La proprietà `ConnectionManagerType` della gestione connessione viene impostata su `EXCEL`.  
  
> [!NOTE]  
>  Non è possibile connettersi a un file di Excel protetto da password.  
  
## <a name="configuration-of-the-excel-connection-manager"></a>Configurazione della gestione connessione Excel  
 Per configurare la gestione connessione Excel, procedere nel modo seguente:  
  
-   Specificare il percorso del file della cartella di lavoro di Excel.  
  
-   Specificare la versione di Excel utilizzata per creare il file.  
  
-   Indicare se la prima riga di dati a cui si accede nei fogli di lavoro o negli intervalli selezionati contiene i nomi delle colonne.  
  
 Se la gestione connessione Excel viene utilizzata da un'origine Excel, i nomi delle colonne saranno inclusi nei dati estratti. Se viene utilizzata da una destinazione Excel, i nomi delle colonne saranno inclusi nei dati scritti.  
  
 La gestione connessione Excel utilizza il provider OLE DB [!INCLUDE[msCoName](../../includes/msconame-md.md)] per Jet 4.0 e il relativo driver ISAM (Indexed Sequential Access Method, metodo di accesso sequenziale indicizzato) di Excel di supporto per stabilire la connessione con le origini dei dati Excel e quindi leggere e scrivere informazioni. Per ulteriori informazioni sul comportamento di questo provider e driver se utilizzato con origini Excel e destinazioni Excel, vedere [Excel source](../data-flow/excel-source.md) ed Excel [Destination](../data-flow/excel-destination.md).  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vedere [Editor gestione connessione Excel](../excel-connection-manager-editor.md).  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../building-packages-programmatically/adding-connections-programmatically.md).  
  
 Per informazioni sul ciclo tramite un gruppo di file Excel, vedere [Esecuzione di un ciclo su file e tabelle di Excel utilizzando un contenitore Ciclo Foreach](../control-flow/foreach-loop-container.md).  
  
## <a name="related-tasks"></a>Attività correlate  
  
-   [Esecuzione di un ciclo su file e tabelle di Excel utilizzando un contenitore Ciclo Foreach](../control-flow/foreach-loop-container.md)  
  
-   [Importare i dati da Excel o esportarli in Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)
  
  
