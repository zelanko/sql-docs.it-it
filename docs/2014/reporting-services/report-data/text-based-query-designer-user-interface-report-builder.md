---
title: Interfaccia utente di Progettazione query basata su testo (Generatore report) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10010"
helpviewer_keywords:
- query designers, text-based
ms.assetid: 89fddca5-bd96-4128-9072-5348d1b6e02c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: bdd12cf49c86cb9a622c1ac546fd755056b5e357
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66106976"
---
# <a name="text-based-query-designer-user-interface-report-builder"></a>Interfaccia utente di Progettazione query basata su testo (Generatore report)
  La finestra Progettazione query basata su testo consente di specificare una query tramite il linguaggio di query supportato dall'origine dati, eseguire la query e visualizzare i risultati in fase di progettazione. È possibile specificare più istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] , la sintassi della query o dei comandi per estensioni per l'elaborazione dati personalizzata e query che vengono specificate come espressioni. Poiché non esegue la pre-elaborazione della query e può gestire qualsiasi tipo di sintassi della query, la finestra Progettazione query basata su testo rappresenta lo strumento di progettazione query predefinito per molti tipi di origine dati.  
  
> [!IMPORTANT]  
>  Gli utenti accedono alle origini dati quando creano ed eseguono query. È necessario concedere autorizzazioni minime per le origini dati, ad esempio autorizzazioni di sola lettura.  
  
 Nella finestra Progettazione query basata su testo vengono visualizzati una barra degli strumenti e i due riquadri seguenti:  
  
-   **Query** Mostra il testo della query e il nome della tabella o della stored procedure, a seconda del tipo di query. Non tutti i tipi di query sono disponibili per tutti i tipi di origine dati. Il nome tabella, ad esempio, è supportato solo per le origini dati di tipo OLE DB.  
  
-   **Risultato** Consente di visualizzare i risultati della query eseguita in fase di progettazione.  
  
## <a name="text-based-query-designer-toolbar"></a>Barra degli strumenti di Progettazione query basata su testo  
 La finestra Progettazione query basata su testo include una sola barra degli strumenti per tutti i tipi di comandi. Nella tabella seguente sono elencati tutti i pulsanti contenuti nella barra degli strumenti con la rispettiva funzione.  
  
|Button|Descrizione|  
|------------|-----------------|  
|**Modifica come testo**|Consente di passare dalla finestra Progettazione query basata su testo alla finestra Progettazione query con interfaccia grafica e viceversa. Le finestre Progettazione query con interfaccia grafica non sono supportate da tutti i tipi di origine dati.|  
|**Importa**|Consente di importare una query esistente da un file o un report. Sono supportati solo i tipi di file con estensione sql e rdl.|  
|![Esecuzione della query](../../analysis-services/media/rsqdicon-run.gif "Esecuzione della query")|Consente di eseguire la query e di visualizzare il set di risultati nel riquadro Risultati.|  
|**Tipo di comando**|Selezionare **Text**, **StoredProcedure**o **TableDirect**. Se una stored procedure dispone di parametri, facendo clic su **Esegui** sulla barra degli strumenti viene visualizzata la finestra di dialogo **Definisci parametri query** ed è possibile inserire i valori desiderati.<br /><br /> Nota: Se una stored procedure restituisce più set di risultati, solo il primo set è utilizzato per popolare il set di dati.|  
  
### <a name="command-type-text"></a>Tipo di comando Text  
 Quando si crea un set di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , per impostazione predefinita viene visualizzata la finestra Progettazione query relazionale. Per passare alla finestra Progettazione query basata su testo, fare clic sul pulsante **Modifica come testo** sulla barra degli strumenti. La finestra Progettazione query basata su testo include due riquadri, il riquadro Query e il riquadro Risultati. Nella figura seguente vengono etichettati tutti i riquadri.  
  
 ![Finestra Progettazione query standard per query di dati relazionali](../../analysis-services/media/rsqd-dsaw-sql-generic.gif "Finestra Progettazione query standard per query di dati relazionali")  
  
 Nella tabella seguente viene descritta la funzione di ogni riquadro.  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Query|Consente di visualizzare il testo della query [!INCLUDE[tsql](../../../includes/tsql-md.md)] . Usare questo riquadro per scrivere o modificare una query [!INCLUDE[tsql](../../../includes/tsql-md.md)] .|  
|Risultato|Consente di visualizzare i risultati della query. Per eseguire la query, fare clic con il pulsante destro del mouse su un riquadro qualsiasi e scegliere **Esegui**oppure fare clic sul pulsante **Esegui** sulla barra degli strumenti.|  
  
#### <a name="example"></a>Esempio  
 La query seguente restituisce l'elenco dei cognomi dal [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] **2008** database `ContactType` table per il `Person` dello schema.  
  
```  
SELECT Name FROM Person.ContactType  
```  
  
 Quando si fa clic su **Esegui** sulla barra degli strumenti, il comando nel riquadro **Query** viene eseguito e i risultati vengono visualizzati nel riquadro **Risultati** . Il set di risultati visualizza un elenco di 20 tipi di contatti, ad esempio, Owner o Sales Agent.  
  
### <a name="command-type-storedprocedure"></a>Tipo di comando StoredProcedure  
 Quando si seleziona **Tipo di comando StoredProcedure**, la finestra Progettazione query basata su testo mostra due riquadri, il riquadro Query e il riquadro Risultati. Immettere il nome della stored procedure nel riquadro Query e fare clic su **Esegui** sulla barra degli strumenti. Se la stored procedure usa parametri, verrà visualizzata la finestra di dialogo **Definisci parametri query** . Immettere i valori dei parametri per la stored procedure. Per ogni parametro di input della stored procedure viene creato un parametro del report.  
  
 Nella figura seguente vengono illustrati i riquadri Query e Risultati quando si esegue una stored procedure. In questo caso, i parametri di input sono costanti.  
  
 ![Stored procedure in Progettazione query basata su testo](../../analysis-services/media/rs-relational-text-sp.gif "Stored procedure in Progettazione query basata su testo")  
  
 Nella tabella seguente viene descritta la funzione di ogni riquadro.  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Query|Visualizza il nome della stored procedure e di qualsiasi parametro di input.|  
|Risultato|Consente di visualizzare i risultati della query. Per eseguire la query, fare clic con il pulsante destro del mouse su un riquadro qualsiasi e scegliere **Esegui**oppure fare clic sul pulsante **Esegui** sulla barra degli strumenti.|  
  
#### <a name="example"></a>Esempio  
 La query seguente chiama il [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] **2008** stored procedure di `uspGetWhereUsedProductID`. Quando si esegue la query, è necessario immettere un valore per il parametro del numero di identificazione del prodotto.  
  
```  
uspGetWhereUsedProductID  
```  
  
 Fare clic sul pulsante **Esegui** (**!**). Quando vengono richiesti i parametri di query, utilizzare la tabella seguente per immettere i valori.  
  
|||  
|-|-|  
|*@StartProductID*|820|  
|*@CheckDate*|20010115|  
  
 Per la data specificata, il set di risultati visualizza un elenco di 13 identificatori del prodotto che hanno utilizzato il numero del componente specificato.  
  
### <a name="command-type-tabledirect"></a>Tipo di comando TableDirect  
 Quando si seleziona **Tipo di comando TableDirect**, la finestra Progettazione query basata su testo mostra due riquadri, il riquadro Query e il riquadro Risultati. Quando si immette una tabella e si fa clic sul pulsante **Esegui** , vengono restituite tutte le colonne della tabella.  
  
#### <a name="example"></a>Esempio  
 Per un tipo di origine dati OLE DB, la query seguente set di dati restituisce un set di risultati per tipi di tutti i contatti nel [!INCLUDE[ssSampleDBobject](../../../includes/sssampledbobject-md.md)] **2008** database.  
  
 `Person.ContactType`  
  
 L'immissione del nome della tabella Person.ContactType, è equivalente alla creazione dell'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] di `SELECT * FROM Person.ContactType`.  
  
## <a name="see-also"></a>Vedere anche  
 [Interfaccia utente di Progettazione query relazionale &#40;Generatore report&#41;](relational-query-designer-user-interface-report-builder.md)   
 [Finestre di progettazione query &#40;Generatore report&#41;](../query-designers-report-builder.md)  
  
  
