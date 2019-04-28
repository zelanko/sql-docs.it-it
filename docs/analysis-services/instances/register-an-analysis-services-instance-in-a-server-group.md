---
title: Registrare un'istanza di Analysis Services in un gruppo di Server | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 45edecf23d0db4580aad134780ee31ea938e887c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62708999"
---
# <a name="register-an-analysis-services-instance-in-a-server-group"></a>Registrare un'istanza di Analysis Services in un gruppo di server
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Se si dispone di un numero elevato di istanze del server Analysis Services, è possibile creare gruppi di server in Management Studio per semplificare l'amministrazione dei server. Lo scopo di un gruppo di server è quello di fornire prossimità tra un gruppo di server correlati all'interno dell'area di lavoro amministrativa. Si supponga, ad esempio, di dover gestire dieci istanze separate di Analysis Services. Raggruppando tali istanze in base a modalità server, criteri relativi al tempo di attività, reparto o area, è possibile visualizzare le istanze che condividono le stesse caratteristiche e connettersi a esse in modo più semplice. È anche possibile aggiungere informazioni descrittive che consentono di ricordare come viene utilizzato il server.  
  
 ![Riquadro Server registrati con i server membri](../../analysis-services/instances/media/ssas-ssms-registerserver.gif "riquadro Server registrati con i server membri")  
  
 È possibile creare i gruppi di server in una struttura gerarchica. Il gruppo Server locali è il nodo radice. Tale gruppo contiene sempre le istanze di Analysis Services in esecuzione nel computer locale. È possibile aggiungere server remoti a qualsiasi gruppo, incluso il gruppo locale.  
  
 Dopo avere creato un gruppo di server, è necessario utilizzare il riquadro Server registrati per visualizzare i server membri e connettersi a essi. Nel riquadro le istanze di SQL Server vengono filtrate in base al tipo di server (Motore di database, Analysis Services, Reporting Services e Integration Services). Fare clic su un tipo di server per visualizzare i gruppi di server creati per tale tipo. Per connettersi a un server specifico in un gruppo, fare doppio clic su un server nel gruppo.  
  
 Le informazioni di connessione definite per il server, incluso il nome del server, vengono rese persistenti con la registrazione del server. Non è possibile modificare le informazioni di connessione o utilizzare il nome registrato in caso di connessione al server utilizzando altri strumenti.  
  
## <a name="create-a-server-group-and-add-registered-servers"></a>Creare un gruppo di server e aggiungere server registrati  
  
1.  In Management Studio scegliere Server registrati dal menu Visualizza per aprire il riquadro Server registrati nell'area di lavoro. Per impostazione predefinita, è già stato creato un gruppo di server locali. Tutte le istanze di Analysis Services in esecuzione nel server locale sono membri di tale gruppo.  
  
2.  Fare clic con il pulsante destro del mouse sul gruppo di server locali, scegliere Nuovo gruppo di server e assegnare un nome al gruppo.  
  
3.  Fare clic con il pulsante destro del mouse sul gruppo di server e scegliere Nuova registrazione server. Immettere il nome di rete di un server locale o remoto, incluso il nome dell'istanza se il server è stato installato come istanza denominata. Facoltativamente, è possibile fornire un nome di server registrato visualizzato in Server registrati. Questo nome viene utilizzato solo in Server registrati. Non è possibile utilizzarlo per rinominare un server né in una stringa di connessione. Un nome di server registrato può essere più descrittivo rispetto al nome del server effettivo o includere altre caratteristiche identificative che consentono di distinguere questo server dagli altri server.  
  
  
