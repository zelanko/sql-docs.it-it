---
title: Editor origine OLE DB (pagina Gestione connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbsourceadapter.connection.f1
helpviewer_keywords:
- OLE DB Source Editor
ms.assetid: 53699902-8699-4547-b56b-a5b2079e98b6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 65d762ffb798d6ec3826a41ff06c73c2011543ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767203"
---
# <a name="ole-db-source-editor-connection-manager-page"></a>Editor origine OLE DB (pagina Gestione connessione)
  Usare la pagina **Gestione connessione** della finestra di dialogo **Editor origine OLE DB** per selezionare la gestione connessione OLE DB per l'origine. Tramite questa pagina è inoltre possibile selezionare una tabella o una vista del database.  
  
> [!NOTE]  
>  Per caricare dati da un'origine dati basata su [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 2007, usare un'origine OLE DB. Non è possibile utilizzare un'origine Excel per caricare dati da un'origine dei dati Excel 2007. Per altre informazioni, vedere [Configura gestione connessione OLE DB](configure-ole-db-connection-manager.md).  
>   
>  Per caricare dati da un'origine dei dati che utilizza [!INCLUDE[msCoName](../includes/msconame-md.md)] Office Excel 2003 o versione precedente, utilizzare un'origine Excel. Per altre informazioni, vedere [Editor origine Excel &#40;pagina Gestione connessione&#41;](../../2014/integration-services/excel-source-editor-connection-manager-page.md).  
  
> [!NOTE]  
>  Il `CommandTimeout` proprietà dell'origine OLE DB non è disponibile nel **Editor origine OLE DB**, ma può essere impostata utilizzando la **Editor avanzato**. Per ulteriori informazioni su questa proprietà, vedere la sezione relativa all'origine Excel in [Proprietà personalizzate OLE DB](data-flow/ole-db-custom-properties.md).  
  
 Per ulteriori informazioni sull'origine OLE DB, vedere [OLE DB Source](data-flow/ole-db-source.md).  
  
## <a name="open-the-ole-db-source-editor-connection-manager-page"></a>Aprire OLE DB Source Editor (pagina Gestione connessione)  
  
1.  Aggiungere l'origine OLE DB al pacchetto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Fare clic con il pulsante destro del mouse sul componente di origine, quindi scegliere **Modifica**.  
  
3.  Fare clic su **Gestione connessione**.  
  
## <a name="static-options"></a>Opzioni statiche  
 **Gestione connessione OLE DB**  
 Selezionare una gestione connessione esistente nell'elenco o crearne una nuova facendo clic su **Nuova**.  
  
 **Nuova**  
 Consente di creare una nuova gestione connessione usando la finestra di dialogo **Configura gestione connessione OLE DB** .  
  
 **Modalità di accesso ai dati**  
 Consente di specificare il metodo per la selezione dei dati dall'origine.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Tabella o vista|Consente di recuperare dati da una tabella o da una vista nell'origine dei dati OLE DB.|  
|Variabile nome vista o nome tabella|Consente di specificare il nome della vista o della tabella in una variabile.<br /><br /> **Informazioni correlate:** [Uso di variabili nei pacchetti](../../2014/integration-services/use-variables-in-packages.md)|  
|Comando SQL|Consente di recuperare dati dall'origine dei dati OLE DB utilizzando una query SQL.|  
|Comando SQL da variabile|Consente di specificare il testo della query SQL in una variabile.|  
  
 **Anteprima**  
 Consente di visualizzare in anteprima i risultati nella finestra di dialogo **Vista dati** . L'**anteprima** supporta la visualizzazione di un massimo di 200 righe.  
  
> [!NOTE]  
>  Quando vengono visualizzati i dati in anteprima, le colonne con tipo definito dall'utente CLR (UDT) non contengono dati. Vengono invece visualizzati i valori \<dimensione valore eccessiva per la visualizzazione> o System.Byte[]. Il primo viene visualizzato se si accede all'origine dati mediante il provider SQL OLE DB, il secondo se si usa il provider [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client.  
  
## <a name="data-access-mode-dynamic-options"></a>Opzioni dinamiche relative alla modalità di accesso ai dati  
  
### <a name="data-access-mode--table-or-view"></a>Modalità di accesso ai dati = Tabella o vista  
 **Nome tabella o vista**  
 Consente di selezionare il nome della tabella o della vista nell'elenco dei nomi disponibili nell'origine dei dati.  
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modalità di accesso ai dati = Variabile nome vista o nome tabella  
 **Nome variabile**  
 Consente di selezionare la variabile che contiene il nome della tabella o vista.  
  
### <a name="data-access-mode--sql-command"></a>Modalità di accesso ai dati = Comando SQL  
 **Testo comando SQL**  
 Immettere il testo di una query SQL, fare clic su **Compila query**per compilare la query o fare clic su **Sfoglia**per individuare il file che contiene il testo della query.  
  
 **Parametri**  
 Se è stata immessa una query con parametri utilizzando ? come segnaposto per il parametro nel testo della query, usare la finestra di dialogo **Imposta parametri query** per eseguire il mapping tra i parametri di input della query e le variabili del pacchetto.  
  
 **Build query**  
 Usare la finestra di dialogo **Generatore query** per creare la query SQL con strumenti grafici.  
  
 **Sfoglia**  
 Usare la finestra di dialogo **Apri** per individuare il file contenente il testo della query SQL.  
  
 **Analizza query**  
 Consente di verificare la sintassi del testo della query.  
  
### <a name="data-access-mode--sql-command-from-variable"></a>Modalità di accesso ai dati = Comando SQL da variabile  
 **Nome variabile**  
 Consente di selezionare la variabile contenente il testo della query SQL.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor origine OLE DB &#40;pagina Colonne&#41;](../../2014/integration-services/ole-db-source-editor-columns-page.md)   
 [Editor origine OLE DB &#40;pagina Output degli errori&#41;](../../2014/integration-services/ole-db-source-editor-error-output-page.md)   
 [Estrazione dei dati tramite l'origine OLE DB](data-flow/extract-data-by-using-the-ole-db-source.md)   
 [Gestione connessione OLE DB](connection-manager/ole-db-connection-manager.md)  
  
  
