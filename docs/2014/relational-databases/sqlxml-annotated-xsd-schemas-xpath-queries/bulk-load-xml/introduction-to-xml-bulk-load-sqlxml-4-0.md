---
title: Introduzione al caricamento bulk XML (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- nontransacted XML Bulk Load operations
- XML Bulk Load [SQLXML], about XML Bulk Load
- bulk load [SQLXML], about bulk load
- transacted XML Bulk Load operations
- streaming XML data
ms.assetid: 38bd3cbd-65ef-4c23-9ef3-e70ecf6bb88a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d257b6eee1fb3adc0ba611f58a1d5eea5adf3f86
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66013384"
---
# <a name="introduction-to-xml-bulk-load-sqlxml-40"></a>Introduzione al caricamento bulk XML (SQLXML 4.0)
  Il caricamento bulk XML è un oggetto COM autonomo che consente di caricare dati XML semistrutturati nelle tabelle di Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 È possibile inserire dati XML in un database [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzando un'istruzione INSERT e la funzione OPENXML. L'utilità di caricamento bulk fornisce tuttavia prestazioni migliori quando è necessario inserire grandi quantità di dati XML.  
  
 Il metodo Execute del modello a oggetti per il caricamento bulk XML accetta due parametri:  
  
-   Uno schema XSD (XML Schema Definition) o uno schema XDR (XML-Data Reduced) con annotazioni. L'utilità di caricamento bulk XML interpreta questo schema di mapping e le annotazioni specificate nello schema per identificare le tabelle di SQL Server nelle quali devono essere inseriti i dati XML.  
  
-   Un documento o un frammento di documento XML (un frammento di documento è un documento privo di un singolo elemento di livello superiore). È possibile specificare un nome file o un flusso dal quale il caricamento bulk XML può leggere.  
  
 Il caricamento bulk XML interpreta lo schema di mapping e identifica le tabelle nelle quali devono essere inseriti i dati XML.  
  
 Si presuppone che l'utente abbia familiarità con le caratteristiche [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] seguenti:  
  
-   Schemi XSD e XDR annotati. Per ulteriori informazioni sugli schemi XSD con annotazioni, vedere [Introduzione agli schemi XSD con Annotazioni &#40;SQLXML 4,0&#41;](../../sqlxml/annotated-xsd-schemas/introduction-to-annotated-xsd-schemas-sqlxml-4-0.md). Per informazioni sugli schemi XDR con annotazioni, vedere [schemi XDR con Annotazioni &#40;deprecati in SQLXML 4,0&#41;](../../sqlxml/annotated-xsd-schemas/annotated-xdr-schemas-deprecated-in-sqlxml-4-0.md).  
  
-   Meccanismi di inserimento bulk [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], quali l'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] BULK INSERT e l'utilità bcp. Per ulteriori informazioni, vedere [BULK INSERT &#40;&#41;Transact-SQL](/sql/t-sql/statements/bulk-insert-transact-sql) e [utilità bcp](../../../tools/bcp-utility.md).  
  
## <a name="streaming-of-xml-data"></a>Flusso dei dati XML  
 Poiché le dimensioni del documento XML di origine possono essere elevate, l'intero documento non viene letto in memoria per l'elaborazione del caricamento bulk. Il caricamento bulk XML interpreta invece i dati XML come un flusso e li legge. Durante la lettura dei dati, l'utilità identifica le tabelle di database, genera i record appropriati dall'origine dati XML, quindi invia i record a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per l'inserimento.  
  
 Il documento XML di ** \<** origine seguente, ad esempio, è costituito dagli elementi Customer>e ** \<Order>** elementi figlio:  
  
```  
<Customer ...>  
    <Order.../>  
    <Order .../>  
     ...  
</Customer>  
...  
```  
  
 Durante la lettura dell'elemento ** \<Customer>** , il caricamento bulk XML genera un record per customerTable. Quando legge il tag di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ** \<fine>/Customer** , il caricamento bulk XML inserisce il record nella tabella in. Allo stesso modo, quando legge l' [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ** \<elemento Order>** , il caricamento bulk XML genera un record per orderTable e quindi inserisce il record nella tabella durante la lettura del ** \<Tag/order>** end.  
  
## <a name="transacted-and-nontransacted-xml-bulk-load-operations"></a>Operazioni di caricamento bulk XML in transazioni e non in transazioni  
 Il caricamento bulk XML può funzionare in modalità transazionale e non transazionale. Le prestazioni sono in genere ottimali se si esegue il caricamento bulk in modalità non transazionale, ovvero la proprietà Transaction è impostata su FALSE, e viene soddisfatta una delle condizioni seguenti:  
  
-   Le tabelle nelle quali si esegue il caricamento bulk dei dati sono vuote e senza indici.  
  
-   Le tabelle includono dati e indici univoci.  
  
 L'approccio non transazionale non garantisce un rollback in caso di errore del processo di caricamento bulk, anche se possono verificarsi rollback parziali. Il caricamento bulk non transazionale è consigliabile quando il database è vuoto. In caso di errore, pertanto, è possibile eseguire una pulizia del database e riavviare il caricamento bulk XML.  
  
> [!NOTE]  
>  In modalità non transazionale il caricamento bulk XML utilizza una transazione interna predefinita e ne esegue il commit. Quando la proprietà Transaction è impostata su TRUE, il caricamento bulk XML non chiama commit per questa transazione.  
  
 Se la proprietà Transaction è impostata su TRUE, il caricamento bulk XML crea i file temporanei, uno per ogni tabella identificata nello schema di mapping. Il caricamento bulk XML archivia innanzitutto i record del documento XML di origine in questi file temporanei. Quindi, un'istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] BULK INSERT recupera tali record dai file e li archivia nelle tabelle corrispondenti. È possibile specificare il percorso per questi file temporanei usando la proprietà TempFilePath. In questo caso, è necessario assicurarsi che l'account di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzato con il caricamento bulk XML disponga di accesso a tale percorso. Se la proprietà TempFilePath non è specificata, per creare i file temporanei viene usato il percorso file predefinito specificato nella variabile di ambiente TEMP.  
  
 Se la proprietà Transaction è impostata su FALSE (impostazione predefinita), il caricamento bulk XML utilizza l'interfaccia OLE DB IRowsetFastLoad per eseguire il caricamento bulk dei dati.  
  
 Se la proprietà ConnectionString imposta la stringa di connessione e la proprietà Transaction è impostata su TRUE, il caricamento bulk XML opera nel proprio contesto di transazione. ad esempio avvia la propria transazione ed esegue il commit o il rollback nel modo appropriato.  
  
 Se la proprietà ConnectionCommand imposta la connessione con un oggetto Connection esistente e la proprietà Transaction è impostata su TRUE, il caricamento bulk XML non esegue un'istruzione COMMIT o ROLLBACK in caso di esito positivo o negativo, rispettivamente. In presenza di un errore, il caricamento bulk XML restituisce il messaggio di errore appropriato. La decisione di eseguire un'istruzione COMMIT o ROLLBACK è delegata al client che ha avviato il caricamento bulk. L'oggetto Connection utilizzato per il caricamento bulk XML deve essere di tipo ICommand o essere un oggetto comando ADO.  
  
 In SQLXML 4,0 non è possibile utilizzare ConnectionObject con la proprietà Transaction impostata su FALSE. La modalità non transazionale non è supportata con un ConnectionObject perché non è possibile aprire più di un'interfaccia IRowsetFastLoad in una sessione passata.  
  
  
