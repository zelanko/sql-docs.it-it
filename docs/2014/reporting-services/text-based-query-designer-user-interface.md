---
title: Interfaccia utente della finestra Progettazione Query basata su testo | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10010"
- sql12.rtp.rptdesigner.dataview.genericquerydesigner.f1
helpviewer_keywords:
- text-based query designer [Reporting Services]
- query designers [Reporting Services], text-based
ms.assetid: 44b7c664-03aa-494e-a484-052b318e810c
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 114b73bf2e15c55669dacea6456dfd9666a485d6
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56288259"
---
# <a name="text-based-query-designer-user-interface"></a>Interfaccia utente di Progettazione query basata su testo
  La finestra Progettazione query basata su testo consente di specificare una query tramite il linguaggio di query supportato dall'origine dati, eseguire la query e visualizzare i risultati in fase di progettazione. È possibile specificare più istruzioni [!INCLUDE[tsql](../includes/tsql-md.md)] , la sintassi della query o dei comandi per estensioni per l'elaborazione dati personalizzata e query che vengono specificate come espressioni. Poiché non esegue la pre-elaborazione della query e può gestire qualsiasi tipo di sintassi della query, la finestra Progettazione query basata su testo rappresenta lo strumento di progettazione query predefinito per molti tipi di origine dati.  
  
 Nella finestra Progettazione query basata su testo vengono visualizzati una barra degli strumenti e i due riquadri seguenti:  
  
-   **Query** Mostra il testo della query, nome della tabella o nome della stored procedure.  
  
-   **Risultato** Consente di visualizzare i risultati della query eseguita in fase di progettazione.  
  
## <a name="text-based-query-designer-toolbar"></a>Barra degli strumenti di Progettazione query basata su testo  
 La finestra Progettazione query basata su testo include una sola barra degli strumenti per tutti i tipi di comandi. Nella tabella seguente sono elencati tutti i pulsanti contenuti nella barra degli strumenti con la rispettiva funzione.  
  
|Button|Descrizione|  
|------------|-----------------|  
|**Modifica come testo**|Consente di passare dalla finestra Progettazione query basata su testo alla finestra Progettazione query con interfaccia grafica e viceversa. Le finestre Progettazione query con interfaccia grafica non sono supportate da tutti i tipi di origine dati.|  
|**Importa**|Consente di importare una query esistente da un file o un report. Sono supportati solo i tipi di file con estensione sql e rdl. Per altre informazioni, vedere [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md).|  
|![Esecuzione della query](../analysis-services/media/rsqdicon-run.gif "Esecuzione della query")|Consente di eseguire la query e di visualizzare il set di risultati nel riquadro Risultati.|  
|**Tipo di comando**|Selezionare **Text**, **StoredProcedure**o **TableDirect**. Se una stored procedure dispone di parametri, facendo clic su **Esegui** sulla barra degli strumenti viene visualizzata la finestra di dialogo **Definisci parametri query** ed è possibile inserire i valori desiderati. Si noti che se una stored procedure restituisce più di un set di risultati, solo il primo set di risultati viene utilizzato per popolare il set di dati.<br /><br /> Il supporto per il tipo di comando varia in base al tipo di origine dati. Ad esempio, solo OLE DB e ODBC supportano **TableDirect**.|  
  
### <a name="command-type-text"></a>Tipo di comando Text  
 Quando si crea un set di dati di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], in Progettazione report viene visualizzata la finestra Progettazione query con interfaccia grafica per impostazione predefinita. Per passare alla finestra Progettazione query basata su testo, fare clic sul pulsante **Modifica come testo** sulla barra degli strumenti. La finestra Progettazione query basata su testo include due riquadri, il riquadro Query e il riquadro Risultati. Nella figura seguente vengono etichettati tutti i riquadri.  
  
 ![Finestra Progettazione query standard per query di dati relazionali](../analysis-services/media/rsqd-dsaw-sql-generic.gif "Finestra Progettazione query standard per query di dati relazionali")  
  
 Nella tabella seguente viene descritta la funzione di ogni riquadro.  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Query|Consente di visualizzare il testo della query [!INCLUDE[tsql](../includes/tsql-md.md)] . Usare questo riquadro per scrivere o modificare una query [!INCLUDE[tsql](../includes/tsql-md.md)] .|  
|Risultato|Consente di visualizzare i risultati della query. Per eseguire la query, fare clic con il pulsante destro del mouse su un riquadro qualsiasi e scegliere **Esegui**oppure fare clic sul pulsante **Esegui** sulla barra degli strumenti.|  
  
#### <a name="example"></a>Esempio  
 La query seguente restituisce l'elenco dei cognomi dalla tabella `Contact` del database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]:  
  
```  
SELECT LastName FROM Person.Person;  
```  
  
 È possibile utilizzare qualsiasi istruzione [!INCLUDE[tsql](../includes/tsql-md.md)] per tipo di comando Text, comprese le istruzioni `EXEC`. La query seguente chiama la stored procedure `uspGetEmployeeManagers` di [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] e restituisce la struttura gerarchica per il dipendente con numero di identificazione 1.  
  
```  
EXEC uspGetEmployeeManagers 1;  
```  
  
 Quando si fa clic su **Esegui** sulla barra degli strumenti, il comando nel riquadro **Query** viene eseguito e i risultati vengono visualizzati nel riquadro **Risultati** .  
  
### <a name="command-type-storedprocedure"></a>Tipo di comando StoredProcedure  
 Quando si seleziona **Tipo di comando StoredProcedure**, la finestra Progettazione query basata su testo mostra due riquadri, il riquadro Query e il riquadro Risultati. Immettere il nome della stored procedure nel riquadro Query e fare clic su **Esegui** sulla barra degli strumenti. Verrà visualizzata la finestra di dialogo Definisci parametri query. Immettere i valori dei parametri per la stored procedure. Per ogni parametro della stored procedure viene creato un parametro di report.  
  
#### <a name="example"></a>Esempio  
 La query seguente chiama la stored procedure `uspGetEmployeeManagers` di [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]. Quando si esegue la query, è necessario immettere un valore per il parametro del numero di identificazione del dipendente.  
  
```  
uspGetEmployeeManagers;  
```  
  
### <a name="command-type-tabledirect"></a>Tipo di comando TableDirect  
 Quando si seleziona **Tipo di comando TableDirect**, la finestra Progettazione query basata su testo mostra due riquadri, il riquadro Query e il riquadro Risultati. Quando si immette una tabella e si fa clic sul pulsante **Esegui** , vengono restituite tutte le colonne della tabella.  
  
#### <a name="example"></a>Esempio  
 La query seguente restituisce un set di risultati per tutti i clienti nel database [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)].  
  
 `Sales.Customer`  
  
 Quando si immette il nome della tabella Sales. Customer, è equivalente alla creazione di [!INCLUDE[tsql](../includes/tsql-md.md)] istruzione `SELECT * FROM Sales.Customer;`.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire query di strumenti di progettazione di Report della finestra di progettazione di SQL Server Data Tools &#40;SSRS&#41;](report-data/query-design-tools-ssrs.md)   
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [Tipo di connessione SQL Server &#40;SSRS&#41;](report-data/sql-server-connection-type-ssrs.md)   
 [Tipo di connessione OLE DB &#40;SSRS&#41;](report-data/ole-db-connection-type-ssrs.md)   
 [Tipo di connessione ODBC &#40;SSRS&#41;](report-data/odbc-connection-type-ssrs.md)   
 [Set di dati condivisi e incorporati del report &#40;Generatore report e SSRS&#41;](report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)   
 [File di configurazione RSReportDesigner](report-server/rsreportdesigner-configuration-file.md)  
  
  
