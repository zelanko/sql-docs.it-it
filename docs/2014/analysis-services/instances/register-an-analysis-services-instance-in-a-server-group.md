---
title: Registrare un'istanza di Analysis Services in un gruppo di server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5fd3826b-8f75-48eb-910c-bf784163e53b
author: minewiskan
ms.author: owend
ms.openlocfilehash: e0b2aa4798dc939ae6a23545dd2b1af4e0162738
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543763"
---
# <a name="register-an-analysis-services-instance-in-a-server-group"></a>Registrare un'istanza di Analysis Services in un gruppo di server
  Se si dispone di un numero elevato di istanze del server Analysis Services, è possibile creare gruppi di server in Management Studio per semplificare l'amministrazione dei server. Lo scopo di un gruppo di server è quello di fornire prossimità tra un gruppo di server correlati all'interno dell'area di lavoro amministrativa. Si supponga, ad esempio, di dover gestire dieci istanze separate di Analysis Services. Raggruppando tali istanze in base a modalità server, criteri relativi al tempo di attività, reparto o area, è possibile visualizzare le istanze che condividono le stesse caratteristiche e connettersi a esse in modo più semplice. È anche possibile aggiungere informazioni descrittive che consentono di ricordare come viene utilizzato il server.

 ![Riquadro Server registrato con i server membri](../media/ssas-ssms-registerserver.gif "Riquadro Server registrato con i server membri")

 È possibile creare i gruppi di server in una struttura gerarchica. Il gruppo Server locali è il nodo radice. Tale gruppo contiene sempre le istanze di Analysis Services in esecuzione nel computer locale. È possibile aggiungere server remoti a qualsiasi gruppo, incluso il gruppo locale.

 Dopo avere creato un gruppo di server, è necessario utilizzare il riquadro Server registrati per visualizzare i server membri e connettersi a essi. Nel riquadro le istanze di SQL Server vengono filtrate in base al tipo di server (Motore di database, Analysis Services, Reporting Services e Integration Services). Fare clic su un tipo di server per visualizzare i gruppi di server creati per tale tipo. Per connettersi a un server specifico in un gruppo, fare doppio clic su un server nel gruppo.

 Le informazioni di connessione definite per il server, incluso il nome del server, vengono rese persistenti con la registrazione del server. Non è possibile modificare le informazioni di connessione o utilizzare il nome registrato in caso di connessione al server utilizzando altri strumenti.

## <a name="create-a-server-group-and-add-registered-servers"></a>Creare un gruppo di server e aggiungere server registrati

1.  In Management Studio scegliere Server registrati dal menu Visualizza per aprire il riquadro Server registrati nell'area di lavoro. Per impostazione predefinita, è già stato creato un gruppo di server locali. Tutte le istanze di Analysis Services in esecuzione nel server locale sono membri di tale gruppo.

2.  Fare clic con il pulsante destro del mouse sul gruppo di server locali, scegliere Nuovo gruppo di server e assegnare un nome al gruppo.

3.  Fare clic con il pulsante destro del mouse sul gruppo di server e scegliere Nuova registrazione server. Immettere il nome di rete di un server locale o remoto, incluso il nome dell'istanza se il server è stato installato come istanza denominata. Facoltativamente, è possibile fornire un nome di server registrato visualizzato in Server registrati. Questo nome viene utilizzato solo in Server registrati. Non è possibile utilizzarlo per rinominare un server né in una stringa di connessione. Un nome di server registrato può essere più descrittivo rispetto al nome del server effettivo o includere altre caratteristiche identificative che consentono di distinguere questo server dagli altri server.


