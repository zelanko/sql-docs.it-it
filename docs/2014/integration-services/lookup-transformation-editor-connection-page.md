---
title: Editor trasformazione ricerca (pagina connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.lookuptransformation.referencetable.f1
helpviewer_keywords:
- Lookup Transformation Editor
ms.assetid: e90d6b69-5a26-43c5-8433-5c3c9588e08c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 7985f713093e839d258a0c9b80bb5d4e6e58f37f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66057944"
---
# <a name="lookup-transformation-editor-connection-page"></a>Editor trasformazione Ricerca (pagina Connessione)
  Usare la pagina **Connessione** della finestra di dialogo **Editor trasformazione Ricerca** per selezionare una gestione connessione. Se si seleziona una gestione connessione OLE DB, viene anche selezionata anche una query, una tabella o una vista per generare il set di dati di riferimento.  
  
 Per ulteriori informazioni sulla trasformazione Ricerca, vedere [Lookup Transformation](data-flow/transformations/lookup-transformation.md).  
  
## <a name="options"></a>Opzioni  
 Le opzioni seguenti sono disponibili quando si selezionano **Full cache** e **Gestione connessione della cache** nella pagina Generale della finestra di dialogo **Editor trasformazione Ricerca** .  
  
 **Gestione connessione della cache**  
 Selezionare una gestione connessione della cache esistente nell'elenco o fare clic su **Nuova**per creare una nuova connessione.  
  
 **Nuova**  
 Consente di creare una nuova gestione connessione nella finestra di dialogo **Editor gestione connessione della cache** .  
  
 Le opzioni seguenti sono disponibili quando si selezionano **Full cache**, **Partial cache**o **No cache**e **Gestione connessione OLE DB**nella pagina Generale della finestra di dialogo **Editor trasformazione Ricerca** .  
  
 **Gestione connessione OLE DB**  
 Selezionare una gestione connessione OLE DB esistente nell'elenco o fare clic su **Nuova**per creare una nuova connessione.  
  
 **Nuova**  
 Consente di creare una nuova connessione usando la finestra di dialogo **Configura gestione connessione OLE DB** .  
  
 **Tabella o vista**  
 Consente di selezionare una tabella o vista esistente nell'elenco o di creare una nuova tabella facendo clic su **Nuova**.  
  
> [!NOTE]  
>  Se si specifica un'istruzione SQL nella pagina **Avanzate** di **Editor trasformazione Ricerca**, tale istruzione sostituisce il nome di tabella selezionato, in quanto ha priorità su di esso. Per altre informazioni, vedere [Editor trasformazione Ricerca &#40;pagina Avanzate&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md).  
  
 **Nuova**  
 Consente di creare una nuova tabella usando la finestra di dialogo **Crea tabella** .  
  
 **Usa i risultati di una query SQL**  
 Questa opzione consente di visualizzare una query preesistente, compilare una nuova query, controllare la sintassi della query e visualizzare in anteprima i risultati della query.  
  
 **Compila query**  
 Consente di creare l'istruzione Transact-SQL da usare per l'esecuzione tramite **Generatore query**, uno strumento grafico usato per creare query tramite la visualizzazione dei dati.  
  
 **Sfoglia**  
 Utilizzare questa opzione per visualizzare una query preesistente salvata in un file.  
  
 **Analizza query**  
 Consente di controllare la sintassi della query.  
  
 **Anteprima**  
 Consente di visualizzare in anteprima i risultati nella finestra di dialogo **Anteprima risultati query** . Questa opzione consente di visualizzare fino a 200 righe.  
  
## <a name="external-resources"></a>Risorse esterne  
 Intervento nel blog sulle [modalità cache di ricerca](https://go.microsoft.com/fwlink/?LinkId=219518) su blogs.msdn.com  
  
## <a name="see-also"></a>Vedere anche  
 [Editor trasformazione Ricerca &#40;pagina Generale&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor trasformazione Ricerca &#40;pagina Colonne&#41;](../../2014/integration-services/lookup-transformation-editor-columns-page.md)   
 [Editor trasformazione Ricerca &#40;pagina Avanzate&#41;](../../2014/integration-services/lookup-transformation-editor-advanced-page.md)   
 [Editor trasformazione Ricerca &#40;pagina Output degli errori&#41;](../../2014/integration-services/lookup-transformation-editor-error-output-page.md)   
 [Trasformazione Ricerca fuzzy](data-flow/transformations/fuzzy-lookup-transformation.md)  
  
  
