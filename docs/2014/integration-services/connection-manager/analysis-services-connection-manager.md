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
ms.openlocfilehash: 8f8ca9ce77e151e761e2cbb1f9128a44784af8ca
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68890397"
---
# <a name="analysis-services-connection-manager"></a>Analysis Services - gestione connessione
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Una gestione connessione consente a un pacchetto di connettersi a un server che esegue [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] un database di o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] a un progetto di che fornisce l'accesso ai dati del cubo e della dimensione. È possibile connettersi a un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solo durante lo sviluppo di pacchetti in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. In fase di esecuzione i pacchetti si connettono al server e al database in cui è stato distribuito il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Sia le attività, ad esempio Esegui DDL [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ed Elaborazione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , sia le destinazioni, ad esempio Training modello di data mining, usano la gestione connessione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Per altre informazioni sui database di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], vedere [Database modelli multidimensionali &#40;SSAS&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/multidimensional-model-databases-ssas).  
  
## <a name="configuration-of-the-analysis-services-connection-manager"></a>Configurazione della Gestione connessione Analysis Services  
 Quando si aggiunge una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] gestione connessione a un pacchetto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea una gestione connessione che in fase di esecuzione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene risolta in una connessione, imposta le proprietà della gestione connessione e la aggiunge alla `Connections` raccolta del pacchetto. La proprietà `ConnectionManagerType` della gestione connessione viene impostata su `MSOLAP100`.  
  
 Per configurare la gestione connessione [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , procedere nel modo seguente:  
  
-   Specificare una stringa di connessione configurata in modo da soddisfare i requisiti del provider Microsoft OLE DB per Analysis Services.  
  
-   Specificare l'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] al quale connettersi.  
  
-   Se ci si connette a un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], specificare la modalità di autenticazione.  
  
-   Indicare se la connessione creata dalla gestione connessione deve essere mantenuta in fase di esecuzione.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Riferimento all'interfaccia utente della finestra di dialogo Aggiungi gestione connessione Analysis Services](add-analysis-services-connection-manager-dialog-box-ui-reference.md)  
  
 Per informazioni sulla configurazione di una gestione connessione a livello di programmazione, vedere l'articolo relativo a <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Aggiunta di connessioni a livello di programmazione](../building-packages-programmatically/adding-connections-programmatically.md).  
  
  
