---
title: Finestra di dialogo Nuovo Database (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.newdatabase.f1
ms.assetid: ddc7804b-acb0-4ae4-a88f-e8cdf704c341
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1bef5adba44a5202e3cc0fc7f2eb48fae08a0e3c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62743719"
---
# <a name="new-database-dialog-box-analysis-services"></a>Finestra di dialogo Nuovo database (Analysis Services)
  Utilizzare la finestra di dialogo **Nuovo database** in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] per creare un nuovo database vuoto di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Per visualizzare la finestra di dialogo **Nuovo database**, fare clic con il pulsante destro del mouse sulla cartella **Database** di un'istanza di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in **Esplora oggetti** e selezionare **Nuovo database**.  
  
## <a name="options"></a>Opzioni  
  
|Nome|Definizione|  
|----------|----------------|  
|**Nome database**|Consente di digitare il nome del nuovo database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
|**Usa nome utente e password specifici**|Selezionare questa opzione per impostare il database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in modo che utilizzi le credenziali di sicurezza di un account utente specificato. Le credenziali specificate verranno usate per l'elaborazione, le query ROLAP, le associazioni out-of-line, i cubi locali, i modelli di data mining, le partizioni remote, gli oggetti collegati e la sincronizzazione dalla destinazione all’origine. Per le istruzioni DMX OPENQUERY verranno invece utilizzate le credenziali dell'utente corrente.|  
|**Nome utente**|Consente di digitare il dominio e il nome dell'account utente che deve essere usato dal database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Utilizzare il formato seguente:<br /><br /> *\<Nome di dominio >* **\\**  *\<nome dell'account utente >*<br /><br /> Nota: Questa opzione è abilitata solo se **usare un nome utente specifico e una password** sia selezionata.|  
|**Password**|Consente di digitare la password per l'account utente specificato in **Nome utente**.|  
|**Usa account del servizio**|Selezionare questa opzione per impostare il database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in modo che utilizzi le credenziali di sicurezza associate al servizio [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] che gestisce il database. Le credenziali dell'account del servizio verranno utilizzate per l'elaborazione, le query ROLAP, le partizioni remote, gli oggetti collegati e la sincronizzazione da un'origine a una destinazione. Per le istruzioni DMX OPENQUERY, i cubi locali e i modelli di data mining, verranno utilizzate le credenziali dell'utente corrente. Questa opzione non è supportata per le associazioni out-of-line.|  
|**Usa credenziali dell'utente corrente**|Selezionare questa opzione per fare in modo che il database [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utilizzi le credenziali di sicurezza dell'utente corrente per le associazioni out-of-line, le istruzioni DMX OPENQUERY, i cubi locali e i modelli di data mining. Questa opzione non è supportata per l'elaborazione, le query ROLAP, le partizioni remote, gli oggetti collegati e la sincronizzazione da un'origine a una destinazione.|  
|**Default**|Selezionare questa opzione per usare le credenziali dell'account utente predefinito per [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Questa opzione comporta l'utilizzo delle impostazioni predefinite del database per l'elaborazione di oggetti, la sincronizzazione dei server e l'esecuzione di istruzioni di data mining **Apri query**. Per altre informazioni su come specificare le impostazioni predefinite a livello di database, vedere [Impostare le proprietà dei database multidimensionali &#40;Analysis Services&#41;](multidimensional-models/set-multidimensional-database-properties-analysis-services.md).<br /><br /> Per impostazione predefinita il `DataSourceImpersonationInfo` del database è impostata su **utilizzare l'account del servizio**. Indipendentemente dal valore della proprietà `DataSourceImpersonationInfo`, verranno utilizzate le credenziali dell'utente corrente per le associazioni out-of-line, le query ROLAP, i cubi locali e i modelli di data mining.|  
|**Descrizione**|Consente di digitare la descrizione del nuovo database di [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .|  
  
## <a name="see-also"></a>Vedere anche  
 [Finestre di progettazione e finestre di dialogo di Analysis Services &#40;dati multidimensionali&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Database modelli multidimensionali &#40;SSAS&#41;](multidimensional-models/multidimensional-model-databases-ssas.md)  
  
  
