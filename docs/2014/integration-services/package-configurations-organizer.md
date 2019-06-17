---
title: Libreria configurazioni pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.packageconfigurationorganizer.f1
helpviewer_keywords:
- Package Configurations Organizer dialog box
ms.assetid: f20ae6cb-9e6a-4d24-88ff-d7a903a4e8d3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d5313118f7949818d341a47744a69cf13c43dbc9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66056970"
---
# <a name="package-configurations-organizer"></a>Libreria configurazioni pacchetto
  Usare la finestra di dialogo **Libreria configurazioni pacchetto** per abilitare le configurazioni dei pacchetti, visualizzarne un elenco per il pacchetto corrente e specificare l'ordine desiderato in base a cui devono essere caricate.  
  
> [!NOTE]  
>  Le configurazioni sono disponibili per il modello di distribuzione del pacchetto. I parametri vengono utilizzati al posto delle configurazioni per il modello di distribuzione del progetto. Con il modello di distribuzione del progetto è possibile distribuire i progetti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] al server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Per altre informazioni sui modelli di distribuzione, vedere [Distribuzione di progetti e pacchetti](packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 Se più configurazioni aggiornano la stessa proprietà, i valori delle configurazioni che si trovano nella parte inferiore dell'elenco sostituiscono quelli delle configurazioni nelle posizioni superiori nell'elenco. L'ultimo valore caricato nella proprietà è quello utilizzato all'esecuzione del pacchetto. Se il pacchetto utilizza una combinazione di configurazione diretta, ad esempio un file di configurazione XML, e indiretta, ad esempio una variabile di ambiente, la configurazione indiretta che punta al percorso della configurazione diretta deve trovarsi in una posizione superiore nell'elenco.  
  
> [!NOTE]  
>  Il caricamento delle configurazioni di pacchetto nell'ordine preferito avviene a partire dall'inizio dell'elenco visualizzato nella finestra di dialogo **Libreria configurazioni pacchetto** fino alla fine dell'elenco. In fase di esecuzione, tuttavia, tali configurazioni potrebbero non essere caricate nell'ordine preferito. In particolare, le configurazioni di pacchetto padre vengono caricate dopo quelle di altri tipi.  
  
 Le configurazioni di pacchetto aggiornano i valori delle proprietà degli oggetti pacchetto in fase di esecuzione. Quando viene caricato un pacchetto, i valori delle configurazioni sostituiscono quelli impostati durante lo sviluppo del pacchetto. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] supporta diversi tipi di configurazione. È possibile, ad esempio, utilizzare un file XML che contiene più configurazioni o una variabile di ambiente che ne contiene una sola. Per altre informazioni, vedere [Configurazioni di pacchetto](../../2014/integration-services/package-configurations.md).  
  
## <a name="options"></a>Opzioni  
 **Abilita configurazioni pacchetto**  
 Selezionare questa opzione per utilizzare le configurazioni con il pacchetto.  
  
 **Nome configurazione**  
 Consente di visualizzare il nome della configurazione.  
  
 **Tipo configurazione**  
 Consente di visualizzare il tipo di percorso in cui sono archiviate le configurazioni.  
  
 **Stringa di configurazione**  
 Consente di visualizzare il percorso in cui sono archiviati i valori della configurazione, che può essere il percorso di un file, il nome di una variabile di ambiente, il nome di una variabile del pacchetto padre, una chiave del Registro di sistema o il nome di una tabella di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **Oggetto di destinazione**  
 Consente di visualizzare il nome dell'oggetto aggiornato dalla configurazione. Se la configurazione è un file di configurazione XML o una tabella di SQL Server, la colonna sarà vuota perché questo tipo di configurazione può includere più oggetti.  
  
 **Proprietà di destinazione**  
 Consente di visualizzare il nome della proprietà modificata dalla configurazione. Se il tipo di configurazione supporta più configurazioni, questa colonna sarà vuota.  
  
 **Aggiungi**  
 Consente di aggiungere una configurazione tramite la Configurazione guidata pacchetto.  
  
 **Modifica**  
 Consente di modificare una configurazione esistente rieseguendo la Configurazione guidata pacchetto.  
  
 **Rimuovi**  
 Selezionare una configurazione e quindi fare clic su **Rimuovi**.  
  
 **Frecce**  
 Selezionare una configurazione e utilizzare le frecce in su o in giù per spostarla verso l'alto o il basso nell'elenco. Le configurazioni vengono caricate nella sequenza in base a cui sono ordinate nell'elenco.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di configurazioni dei pacchetti](../../2014/integration-services/create-package-configurations.md)  
  
  
