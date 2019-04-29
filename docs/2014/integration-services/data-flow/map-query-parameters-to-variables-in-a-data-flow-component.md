---
title: Mapping dei parametri di query a variabili in un componente flusso di dati | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- queries [Integration Services], parameter mapping
- parameters [Integration Services]
- mapping query parameters to variables [Integration Services]
- variables [Integration Services], mapping parameters to
ms.assetid: 5e26977c-758c-46d6-acf1-4fd9238f0950
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 92caab2b0631c80403c7367aeb98ae001a5e11eb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62901630"
---
# <a name="map-query-parameters-to-variables-in-a-data-flow-component"></a>Mapping dei parametri di query a variabili in un componente del flusso di dati
  Quando viene configurata l'origine OLE DB per utilizzare query con parametri, è possibile eseguire il mapping dei parametri alle variabili.  
  
 L'origine OLE DB utilizza query con parametri per filtrare i dati quando l'origine si collega a un'origine dati.  
  
### <a name="to-map-a-query-parameter-to-a-variable"></a>Per eseguire il mapping di un parametro di query a una variabile  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di dati** e quindi dalla **Casella degli strumenti**trascinare l'origine OLE DB sull'area di progettazione.  
  
4.  Fare clic con il pulsante destro del mouse sull'origine OLE DB e quindi scegliere **Modifica**.  
  
5.  In **Editor origine OLE DB**, selezionare la gestione connessione OLE DB da usare per la connessione all'origine dei dati oppure fare clic su **Nuova** per creare una nuova gestione connessione OLE DB.  
  
6.  Selezionare l'opzione **Comando SQL** per la modalità di accesso ai dati e quindi immettere una query con parametri nella casella **Testo comando SQL** .  
  
7.  Fare clic su **Parametri**.  
  
8.  Nella finestra di dialogo **Imposta parametri query** eseguire il mapping di ogni parametro nell'elenco **Parametri** a una variabile nell'elenco **Variabili** oppure fare clic su **\<Nuova variabile>** per creare una nuova variabile. Fare clic su **OK**.  
  
    > [!NOTE]  
    >  Sono disponibili per il mapping solo le variabili di sistema e le variabili definite dall'utente nell'ambito del pacchetto, di un contenitore padre quale Ciclo Foreach o dell'attività Flusso di dati che contiene il componente del flusso di dati. La variabile deve avere un tipo di dati compatibile con la colonna nella clausola WHERE a cui è assegnato il parametro.  
  
9. Facendo clic su **Anteprima** è possibile visualizzare fino a 200 righe di dati restituiti dalla query.  
  
10. Per salvare il pacchetto aggiornato, scegliere **Salva elementi selezionati** dal menu **File** .  
  
## <a name="see-also"></a>Vedere anche  
 [Origine OLE DB](ole-db-source.md)   
 [Trasformazione Ricerca](transformations/lookup-transformation.md)  
  
  
