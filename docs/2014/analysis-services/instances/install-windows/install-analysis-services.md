---
title: Installare Analysis Services in modalità tabulare | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: cd6ac80d-b735-4e3e-a024-489f1409ad33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f8690c252ddb1b91cd939044ee4f0ccc3a6f4a60
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62703632"
---
# <a name="install-analysis-services-in-tabular-mode"></a>Installare Analysis Services in modalità Tabella
  Se si sta installando Analysis Services per utilizzare le nuove funzionalità di modelli tabulari, è necessario installarlo in una modalità server che supporti tale tipo di modello. La modalità server è Tabella ed è configurata durante l'installazione.  
  
 Dopo aver installato il server in questa modalità, è possibile utilizzare le soluzioni host compilate nella progettazione di modelli tabulari. Un server in modalità tabulare è necessario se si desidera l'accesso ai dati dei modelli tabulari sulla rete.  
  
 È possibile specificare la modalità Tabella nell'installazione guidata o in un'installazione dalla riga di comando. Nelle sezioni seguenti vengono descritte le diverse modalità.  
  
## <a name="installation-wizard"></a>Installazione guidata  
 Nel seguente elenco sono riportate le pagine dell'installazione guidata di SQL Server che vengono utilizzate per installar Analysis Services in modalità Tabella.  
  
1.  Selezionare **Analysis Services** dall'albero delle funzionalità nell'installazione.  
  
     ![Albero delle funzionalità di installazione che mostra i servizi Analsyis](../../../sql-server/install/media/ssas-setupas.gif "albero delle funzionalità di installazione che mostra Analsyis Services")  
  
2.  Nella pagina Configurazione di Analysis Services, assicurarsi di selezionare **modalità tabulare**.  
  
     ![Pagina di installazione con le opzioni di configurazione di Analysis Services](../../../sql-server/install/media/ssas-setupasconfig.gif "pagina di installazione con le opzioni di configurazione di Analysis Services")  
  
 Tramite questa modalità viene utilizzato il motore di analisi in memoria xVelocity (VertiPaq) che costituisce l'archivio predefinito per i modelli tabulari distribuiti in Analysis Services. Una volta distribuite le soluzioni del modello tabulare nel server, è possibile configurare selettivamente le soluzioni tabulari per utilizzare l'archivio su disco DirectQuery in alternativa allo spazio di archiviazione associato alla memoria.  
  
## <a name="command-line-setup"></a>Installazione dalla riga di comando  
 Nell'installazione di SQL Server è incluso un nuovo parametro (`ASSERVERMODE`) mediante il quale viene specificata la modalità server. Nell'esempio seguente viene illustrata un'istallazione dalla riga di comando che installa Analysis Services nella modalità server Tabella.  
  
```  
  
Setup.exe /q /IAcceptSQLServerLicenseTerms /ACTION=install /FEATURES=AS /ASSERVERMODE=TABULAR /INSTANCENAME=ASTabular /INDICATEPROGRESS/ASSVCACCOUNT=<DomainName\UserName> /ASSVCPASSWORD=<StrongPassword> /ASSYSADMINACCOUNTS=<DomainName\UserName>   
```  
  
 `INSTANCENAME` deve contenere meno di 17 caratteri.  
  
 Tutti i valori segnaposto degli account devono essere sostituiti con password e account validi.  
  
 Strumenti come SQL Server Management Studio o [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)] non vengono installati utilizzando la sintassi della riga di comando di esempio fornita. Per altre informazioni sull'aggiunta di funzionalità, vedere [installare SQL Server 2014 dal Prompt dei comandi](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
 `ASSERVERMODE` supporta la distinzione tra maiuscole e minuscole.  È necessario esprimere tutti i valori in lettere maiuscole. Nella tabella seguente vengono descritti i valori validi per `ASSERVERMODE`.  
  
|Value|Descrizione|  
|-----------|-----------------|  
|MULTIDIMENSIONAL|Rappresenta il valore predefinito. Se `ASSERVERMODE` non viene impostato, il server viene installato nella modalità server Multidimensionale.|  
|POWERPIVOT|Questo valore è facoltativo. In pratica, se si imposta il parametro `ROLE`, la modalità del server è automaticamente impostata su 1, rendendo `ASSERVERMODE` facoltativo per un'installazione di PowerPivot per SharePoint. Per altre informazioni, vedere [installare PowerPivot dal Prompt dei comandi](../../../sql-server/install/install-powerpivot-from-the-command-prompt.md).|  
|TABULAR|Questo valore è obbligatorio se si installa Analysis Services nella modalità Tabella tramite l'installazione dalla riga di comando.|  
  
## <a name="see-also"></a>Vedere anche  
 [Determinare la modalità server di un'istanza di Analysis Services](../determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Configurare l'accesso DirectQuery per un Database modello tabulare o In memoria](../../tabular-models/enable-directquery-mode-in-ssms.md)   
 [Modellazione tabulare &#40;tabulare di SSAS&#41;](../../tabular-models/tabular-models-ssas.md)  
  
  
