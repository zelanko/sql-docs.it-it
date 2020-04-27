---
title: Report per la risoluzione dei problemi relativi all'esecuzione dei pacchetti | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 8fc476ac-bd69-434e-9636-70776e0b3b6c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1c1a59d9e77806666c487b0778edd574bcaa5e42
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62926307"
---
# <a name="troubleshooting-reports-for-package-execution"></a>Risoluzione dei problemi relativi ai report per l'esecuzione del pacchetto
  Nella versione corrente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] sono disponibili report standard per il monitoraggio e la risoluzione dei problemi relativi ai pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] distribuiti nel catalogo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Due di queste report relativi a pacchetti, in particolare, consentono di visualizzare lo stato di esecuzione dei pacchetti e di identificare la causa di errori di esecuzione.  
  
-   **Dashboard Integration Services** : questo report include una panoramica di tutte le esecuzioni del pacchetto nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nelle ultime 24 ore. Nel report vengono visualizzate informazioni quali Stato, Tipo operazione, Nome pacchetto e così via, per ogni pacchetto.  
  
     I parametri Ora di inizio, Ora di fine e Durata possono essere interpretati nel modo seguente:  
  
    -   Se il pacchetto è ancora in esecuzione, Durata = ora corrente - Ora di inizio  
  
    -   Se il pacchetto è stato completato, Durata = Ora di fine - Ora di inizio  
  
     Per ogni pacchetto eseguito nel server, il dashboard consente all'utente di effettuare un ingrandimento per trovare dettagli specifici sugli errori di esecuzione del pacchetto che potrebbero essersi verificati. Ad esempio, selezionare **Panoramica** per visualizzare una panoramica ad alto livello dello stato delle attività nell'esecuzione, o **Tutti i messaggi** per visualizzare i messaggi dettagliati acquisiti durante l'esecuzione del pacchetto.  
  
     È possibile filtrare la tabella visualizzata in qualsiasi pagina facendo clic su **Filtro** e selezionando i criteri nella finestra di dialogo **Impostazioni filtro** . I criteri di filtro disponibili dipendono dai dati visualizzati. È possibile modificare l'ordinamento del report facendo clic sulla relativa icona nella finestra di dialogo **Impostazioni filtro** .  
  
-   **Attività - Tutte le esecuzioni**: in questo report viene visualizzato un riepilogo di tutte le esecuzioni di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che sono state eseguite nel server. Nel riepilogo vengono visualizzate informazioni per ogni esecuzione, ad esempio, stato, ora di inizio e ora di fine. Ogni voce del riepilogo include collegamenti a ulteriori informazioni relative all'esecuzione, inclusi i messaggi generati durante l'esecuzione e i dati relativi alle prestazioni. Come per il Dashboard Integration Services, è possibile applicare un filtro alla tabella per limitare le informazioni visualizzate.  
  
## <a name="related-tasks"></a>Attività correlate  
 [Visualizzare i report per il server Integration Services](../view-reports-for-the-integration-services-server.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 [Report per il server Integration Services](../reports-for-the-integration-services-server.md)  
  
 [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](troubleshooting-tools-for-package-execution.md)  
  
  
