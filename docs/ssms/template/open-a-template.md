---
title: Aprire un modello | Microsoft Docs
ms.custom: ''
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
ms.openlocfilehash: c52d9b58a3fb738222c78dd57e9d45634963fbde
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68266759"
---
# <a name="open-a-template"></a>Aprire un modello
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
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
[Visualizza](../../ssms/template/template-explorer.md)  
[Sostituire i parametri del modello](../../ssms/template/replace-template-parameters.md)  
  
