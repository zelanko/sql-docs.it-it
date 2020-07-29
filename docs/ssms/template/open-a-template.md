---
title: Aprire un modello
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- templates [Transact-SQL], opening
- opening templates
ms.assetid: 605b0f4c-5ba1-4249-ad1c-6341df77cd7a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 419f3d4fe4d91165782e10e3dc638b8488ea05e5
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86001549"
---
# <a name="open-a-template"></a>Aprire un modello
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
È possibile aprire un modello da Esplora modelli.  
  
## <a name="to-open-a-template-from-template-explorer"></a>Per aprire un modello da Esplora modelli  
È possibile aprire modelli da Esplora modelli.  
  
1.  Per aprire Esplora modelli scegliere **Esplora modelli** dal menu **Visualizza**.  
  
2.  Nell'elenco delle categorie di modello espandere la categoria che contiene il modello che si desidera aprire.  
  
3.  Sono disponibili tre modi per aprire il modello:  
  
    1.  Fare doppio clic sul modello per aprirlo nella finestra dell'editor di codice.  
  
    2.  Fare clic con il pulsante destro del mouse sul modello e selezionare **Apri** nella finestra dell'editor di codice.  
  
    3.  Trascinare il modello nella finestra dell'editor di codice per aggiungere il relativo codice al contenuto della finestra dell'editor.  
  
Dopo avere aperto il modello, usare la finestra di dialogo **Sostituisci parametri modello** per sostituire i parametri del modello con i valori appropriati.  
  
Se in seguito all'apertura di un modello viene aperta una nuova finestra dell'editor, la finestra verrà aperta con le credenziali della connessione attiva corrente. Ad esempio, se è attiva un'istanza del [!INCLUDE[ssDE](../../includes/ssde_md.md)] in Esplora oggetti quando si apre il modello CREATE DATABASE, verrà aperta una nuova finestra dell'editor utilizzando una connessione a tale istanza. In assenza di connessione attiva, in [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] verrà visualizzata una finestra di dialogo di accesso.  
  
## <a name="see-also"></a>Vedere anche  
[Esplora modelli](../../ssms/template/template-explorer.md)  
[Sostituire i parametri del modello](../../ssms/template/replace-template-parameters.md)  
  
