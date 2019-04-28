---
title: 'Gestione dominio: Elenco di domini | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.dm.domainlist.f1
ms.assetid: 8df305f0-97ea-4226-811b-979ed862e1f0
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 2a68300e15c1ae05bcd6ae83228565842a854234
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62792748"
---
# <a name="domain-management-domain-list"></a>Gestione dominio: Elenco di domini
  In questo argomento vengono descritti i controlli dell'elenco Domini nella pagina **Gestione dominio** in [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Utilizzare questo riquadro per selezionare un dominio su cui eseguire le operazioni di gestione. Lo stesso riquadro viene utilizzato per tutte le pagine a schede della pagina **Gestione dominio** .  
  
## <a name="options"></a>Opzioni  
  
### <a name="domains-list"></a>Elenco domini  
 **Dominio**  
 In questo elenco vengono visualizzati tutti i domini della Knowledge Base. Le operazioni che si eseguono nelle pagine a schede nel riquadro a destra saranno eseguite sul dominio selezionato nell'elenco. Per ulteriori informazioni, vedere  
  
 **Creazione di un dominio composito**  
 Consente di creare un nuovo dominio composito nella Knowledge Base. Con questo comando viene visualizzata la finestra di dialogo **Crea un dominio composito** . Questo comando è disponibile facendo clic con il pulsante destro del mouse su un dominio o facendo clic sull'icona sopra l'elenco di domini. Per altre informazioni, vedere [Creazione di un dominio composito](../../2014/data-quality-services/create-a-composite-domain.md).  
  
 **Creazione di un dominio**  
 Consente di creare un nuovo dominio nella Knowledge Base. Con questo comando viene visualizzata la finestra di dialogo **Crea dominio** . Questo comando è disponibile facendo clic con il pulsante destro del mouse su un dominio o facendo clic sull'icona sopra l'elenco di domini. Per altre informazioni, vedere [Creazione di un dominio](../../2014/data-quality-services/create-a-domain.md).  
  
 **Crea copia del dominio selezionato**  
 Consente di creare una copia esatta del dominio selezionato e di aggiungerla alla Knowledge Base. Il nome sarà il nome del dominio dal quale è stata creata la copia più " - Copy" aggiunto al nome. Questo comando è disponibile facendo clic con il pulsante destro del mouse su un dominio e quindi facendo clic su **Crea copia**o facendo clic sull'icona sopra l'elenco di domini. Non è disponibile per un dominio composito.  
  
 **Importa dominio da file di dati**  
 Consente di importare un dominio da un file DQS. Con questo comando viene visualizzata la finestra di dialogo **Importa da file di dati** che consente di esplorare il file system e di selezionare un file DQS per un singolo dominio o un dominio composito. Questo comando è disponibile facendo clic sull'icona sopra l'elenco di domini. Per altre informazioni, vedere [Consente di importare un dominio da un file DQS](../../2014/data-quality-services/import-a-domain-from-a-dqs-file.md).  
  
 **Elimina dominio**  
 Consente di eliminare il dominio selezionato dalla Knowledge Base. Con questo comando viene visualizzata la finestra di dialogo **SQL Server Data Quality Services** . Se si fa clic **Sì**, il dominio e tutti i relativi dati verranno eliminati in modo definitivo. Questo comando è disponibile facendo clic con il pulsante destro del mouse su un dominio o facendo clic sull'icona sopra l'elenco di domini.  
  
 **Creazione di un dominio collegato**  
 Consente di creare un dominio collegato al dominio selezionato. Con questo comando viene visualizzata la finestra di dialogo **Crea dominio** . Questo comando è disponibile facendo clic con il pulsante destro del mouse su un dominio e quindi scegliendo **Crea dominio collegato** . Il dominio al quale si effettua il collegamento viene visualizzato nella finestra di dialogo Crea dominio. Il comando non è disponibile per un dominio composito. Non è previsto alcun comando per annullare il collegamento tra due domini. Per eseguire questa operazione, è necessario eliminare il dominio collegato. Non è possibile creare un dominio collegato a un dominio collegato. Per altre informazioni, vedere [Crea dominio collegato](../../2014/data-quality-services/create-a-linked-domain.md).  
  
 Un dominio collegato dispone degli stessi valori del dominio al quale è stato collegato. Solo il nome e le proprietà del dominio sono diversi. Se si modificano una regola di dominio, un valore di dominio, un collegamento ai dati di riferimento o una relazione basata su termini nel dominio a cui è stato effettuato il collegamento, si modificheranno anche la regola di dominio, il valore di dominio, il collegamento ai dati di riferimento o la relazione basata su termini nel dominio collegato. Inoltre, se si modifica un valore nel dominio collegato, la modifica sarà apportata anche nel dominio a cui è stato effettuato il collegamento.  
  
 **Esporta Knowledge Base**  
 Consente di esportare l'intera Knowledge Base in un file DQS. Con questo comando viene visualizzata la finestra di dialogo **Esporta in file di dati** . Questo comando è disponibile facendo clic sull'icona **Esporta dati Knowledge Base** all'inizio della pagina o in **Esporta** nel menu di scelta rapida dei domini nel riquadro dell'elenco di domini. Per altre informazioni, vedere [Esportazione di una Knowledge Base in un file DQS](../../2014/data-quality-services/export-a-knowledge-base-to-a-dqs-file.md).  
  
 **Esporta dominio**  
 Consente di esportare il dominio in un file DQS. Con questo comando viene visualizzata la finestra di dialogo **Esporta in file di dati** . Questo comando è disponibile nel menu **Esporta** della barra dei menu all'inizio della pagina o facendo clic con il pulsante destro del mouse nel riquadro dell'elenco di domini. Per altre informazioni, vedere [Esportazione di un dominio in un file DQS](../../2014/data-quality-services/export-a-domain-to-a-dqs-file.md).  
  
  
