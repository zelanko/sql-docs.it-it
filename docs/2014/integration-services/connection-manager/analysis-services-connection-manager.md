---
title: Gestione connessione Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- connections [Integration Services], Analysis Services
- connection managers [Integration Services], Analysis Services
- Analysis Services connection manager
ms.assetid: 9f9cadad-a1d0-4db5-98f5-df5dbbec1be4
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 985e5896498d6bb6847ce01af7d3fd04bea50a24
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58376159"
---
# <a name="analysis-services-connection-manager"></a>Analysis Services - gestione connessione
  Una gestione connessione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] consente la connessione di un pacchetto a un server che esegue un database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oppure a un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che permette di accedere ai dati di cubi e dimensioni. È possibile connettersi a un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solo durante lo sviluppo di pacchetti in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. In fase di esecuzione i pacchetti si connettono al server e al database in cui è stato distribuito il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Sia le attività, ad esempio Esegui DDL [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ed Elaborazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], sia le destinazioni, ad esempio Training modello di data mining, usano la gestione connessione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 Per altre informazioni sui database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [Database modelli multidimensionali &#40;SSAS&#41;](../../analysis-services/multidimensional-models/multidimensional-model-databases-ssas.md).  
  
## <a name="configuration-of-the-analysis-services-connection-manager"></a>Configurazione della Gestione connessione Analysis Services  
 Quando si aggiunge un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gestione connessione a un pacchetto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una connessione di gestione che viene risolto come un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] connessione in fase di esecuzione, imposta le proprietà di gestione connessione e aggiunge la gestione connessione il `Connections` raccolta nel pacchetto. La proprietà `ConnectionManagerType` della gestione connessione viene impostata su `MSOLAP100`.  
  
 Per configurare la gestione connessione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , procedere nel modo seguente:  
  
-   Specificare una stringa di connessione configurata in modo da soddisfare i requisiti del provider Microsoft OLE DB per Analysis Services.  
  
-   Specificare l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] al quale connettersi.  
  
-   Se ci si connette a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], specificare la modalità di autenticazione.  
  
-   Indicare se la connessione creata dalla gestione connessione deve essere mantenuta in fase di esecuzione.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione Analysis Services](add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  
