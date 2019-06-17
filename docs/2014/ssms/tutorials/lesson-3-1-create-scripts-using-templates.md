---
title: Creare script usando i modelli | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: ed48014c-3fc9-48ff-8c0f-8d1822195f14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8387cdaf85d6fd7750229fda86c8cb3122b61d90
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913555"
---
# <a name="create-scripts-using-templates"></a>Creare script utilizzando i modelli
  Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] include numerosi modelli di script contenenti istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] per eseguire le attività più comuni. Tali modelli contengono parametri per i valori specificati dall'utente, ad esempio un nome di tabella. L'utilizzo dei parametri consente di digitare il nome una sola volta e quindi copiarlo automaticamente in tutte le posizioni richieste all'interno dello script. È possibile creare modelli personalizzati per supportare gli script che vengono scritti più di frequente. È inoltre possibile riorganizzare l'albero dei modelli spostandoli o creando nuove cartelle dove contenerli. In questa esercitazione verrà utilizzato un modello per creare un database e verranno specificati i parametri del modello.  
  
## <a name="using-templates"></a>Utilizzo dei modelli  
  
#### <a name="to-create-a-script-using-a-template"></a>Per creare uno script utilizzando un modello  
  
1.  In [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]scegliere **Esplora modelli** dal menu **Visualizza**.  
  
2.  In Esplora modelli i modelli sono organizzati in gruppi. Espandere **Database**e quindi fare doppio clic su **Crea database**.  
  
3.  Nella finestra di dialogo **Connetti al motore di database** specificare le informazioni di connessione e quindi fare clic su **Connetti**. Viene visualizzata una nuova finestra dell'editor di query che include il contenuto del modello **Crea database** .  
  
4.  Scegliere **Imposta valori per parametri modello** dal menu **Query**.  
  
5.  Nella finestra di dialogo **Specifica valori per parametri modello** la colonna **Valore** contiene un valore consigliato per il parametro **Database_Name** . Nella casella del parametro **Nome database** digitare **Marketing**e quindi fare clic su **OK**. Si noti che il parametro "Marketing" viene inserito in numerosi punti dello script.  
  
## <a name="next-task-in-lesson"></a>Attività successiva della lezione  
 [Creare modelli personalizzati](lesson-3-2-create-custom-templates.md)  
  
  
