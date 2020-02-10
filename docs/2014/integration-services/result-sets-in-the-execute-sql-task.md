---
title: Set di risultati nell'attività Esegui SQL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- result sets [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: 62605b63-d43b-49e8-a863-e154011e6109
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8efb049292caecf21f38ef5bc5a7392138bdcf5a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66056425"
---
# <a name="result-sets-in-the-execute-sql-task"></a>Set di risultati nell’attività Esegui SQL
  La restituzione di un set di risultati all'attività Esegui SQL in un pacchetto di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] dipende dal tipo di comando SQL utilizzato dall'attività. Se si utilizzano ad esempio le istruzioni SELECT, viene in genere restituito un set di risultati, mentre questo non avviene per le istruzioni INSERT.  
  
 Anche il contenuto del set di risultati varia in base al comando SQL. Il set di risultati restituito da un'istruzione SELECT può ad esempio contenere zero, una o più righe. Il set di risultati di un'istruzione SELECT che restituisce un conteggio o una somma contiene tuttavia una sola riga.  
  
 Per usare i set di risultati in un'attività Esegui SQL non è sufficiente sapere se il comando SQL restituisce un set di risultati né conoscere il contenuto di tale set di risultati. Sono previsti ulteriori requisiti e linee guida per usare correttamente i set di risultati nell'attività Esegui SQL. Nella parte restante di questo argomento vengono illustrati tali requisiti e linee guida:  
  
-   [Specifica di un tipo di set di risultati](#Result_set_type)  
  
-   [Popolamento di una variabile con un set di risultati](#Populate_variable_with_result_set)  
  
-   [Configurazione dei set di risultati nell'editor attività Esegui SQL](#Configure_result_sets)  
  
##  <a name="Result_set_type"></a>Specifica di un tipo di set di risultati  
 L'attività Esegui SQL supporta i tipi di set di risultati seguenti:  
  
-   Se la query non restituisce risultati, sarà usato il set di risultati **Nessuno** . Questo set di risultati può essere usato ad esempio per le query che aggiungono, modificano ed eliminano record in una tabella.  
  
-   Se la query restituisce una sola riga, sarà usato il set di risultati **Riga singola** . Questo set di risultati può ad esempio essere usato per un'istruzione SELECT che restituisce un conteggio o una somma.  
  
-   Se la query restituisce più righe, sarà usato il set di risultati **Set dei risultati completo** . Questo set di risultati può ad esempio essere usato per un'istruzione SELECT che recupera tutte le righe di una tabella.  
  
-   Se la query restituisce un set di risultati in formato XML, sarà usato il set di risultati **XML** . Questo set di risultati può ad esempio essere usato per un'istruzione SELECT che include una clausola FOR XML.  
  
 Se nell'attività Esegui SQL è usato il **Set dei risultati completo** e la query restituisce più set di righe, l'attività restituisce solo il primo di tali set. Se questo set di righe genera un errore, l'attività segnala l'errore. Se altri set di righe generano errori, l'attività non li segnala.  
  
##  <a name="Populate_variable_with_result_set"></a>Popolamento di una variabile con un set di risultati  
 Se il set di risultati restituito da una query è una riga singola, un set di righe o di tipo XML, sarà possibile associarlo a una variabile definita dall'utente.  
  
 Se il tipo di set di risultati è **Riga singola**, è possibile associare una colonna nel risultato restituito a una variabile usando il nome della colonna come nome del set di risultati oppure usare la posizione ordinale della colonna nell'elenco di colonne come nome del set di risultati. Il nome del set di risultati per la query `SELECT Color FROM Production.Product WHERE ProductID = ?` , ad esempio, potrebbe essere **Color** o **0**. Se la query restituisce più colonne e si desidera accedere ai valori in tutte le colonne, è necessario associare ogni colonna a una variabile diversa. Se si esegue il mapping delle colonne alle variabili usando numeri come nomi del set di risultati, i numeri riflettono l'ordine in cui le colonne vengono visualizzate nell'elenco di colonne della query. Nella query `SELECT Color, ListPrice, FROM Production.Product WHERE ProductID = ?`, ad esempio, viene usato 0 per la colonna **Color** e 1 per la colonna **ListPrice** . La possibilità di usare un nome di colonna come nome di un set di risultati dipende dal provider per il quale l'attività è configurata. Non tutti i provider permettono l'uso di nomi di colonna.  
  
 Alcune query che restituiscono un singolo valore non includono nomi di colonna. L'istruzione `SELECT COUNT (*) FROM Production.Product` non restituisce ad esempio alcun nome di colonna. Per accedere al risultato restituito è possibile usare la posizione ordinale, 0, come nome del risultato. Per accedere al risultato restituito in base al nome della colonna, la query deve includere una clausola AS \<nome alias> che specifichi un nome di colonna. Nell'istruzione `SELECT COUNT (*)AS CountOfProduct FROM Production.Product`è specificato il nome di colonna **CountOfProduct** . Per accedere alla colonna del risultato restituito è quindi possibile usare il nome di colonna, **CountOfProduct** , o la posizione ordinale, 0.  
  
 Se il set di risultati è di tipo **Set dei risultati completo** o **XML**, sarà necessario usare 0 come nome del set di risultati.  
  
 Quando si esegue il mapping di una variabile a un set di risultati con il tipo di set di risultati **Riga singola** , la variabile deve avere un tipo di dati compatibile con quello della colonna contenuta nel set di risultati. Non è possibile, ad esempio, eseguire il mapping di un set di risultati che contiene una colonna con un tipo di dati `String` a una variabile con un tipo di dati numerico. Quando si imposta la proprietà **TypeConversionMode** su `Allowed`, l'attività Esegui SQL tenterà di convertire il parametro di output e i risultati della query nel tipo di dati della variabile a cui sono assegnati i risultati.  
  
 È possibile eseguire il mapping di un set di risultati XML solo a una variabile con il tipo di dati `String` o `Object`. Se la variabile ha il tipo di dati `String`, l'attività Esegui SQL restituisce una stringa e l'origine XML può utilizzare i dati XML. Se la variabile ha il tipo di dati `Object`, l'attività Esegui SQL restituisce un oggetto DOM (Document Object Model).  
  
 Un **set di risultati completo** deve eseguire il `Object` mapping a una variabile del tipo di dati. Il risultato restituito è un oggetto set di righe. È possibile usare un contenitore Ciclo ForEach per estrarre i valori di riga della tabella archiviati nella variabile Object nelle variabili del pacchetto e quindi usare un'attività Script per scrivere in un file i dati archiviati nelle variabili del pacchetto. Per una dimostrazione dell'esecuzione di questa operazione tramite un contenitore Ciclo ForEach e un'attività Script, vedere l'esempio CodePlex, relativo all' [esecuzione di parametri SQL e set di risultati](https://go.microsoft.com/fwlink/?LinkId=157863)sul sito Web msftisprodsamples.codeplex.com.  
  
 Nella tabella seguente è disponibile un riepilogo dei tipi di dati delle variabili di cui è possibile eseguire il mapping a set di risultati.  
  
|Tipo di set di risultati|Tipo di dati della variabile|Tipo di oggetto|  
|---------------------|---------------------------|--------------------|  
|Riga singola|Qualunque tipo compatibile con la colonna del tipo nel set di risultati.|Non applicabile|  
|Set dei risultati completo|`Object`|Se l'attività usa una gestione connessione nativa, incluse le gestioni connessioni ADO, OLE DB, Excel e ODBC, l'oggetto restituito è un oggetto `Recordset` ADO.<br /><br /> Se nell'attività viene usata una gestione connessione gestita, ad esempio la gestione connessione [!INCLUDE[vstecado](../includes/vstecado-md.md)], l'oggetto restituito è un oggetto `System.Data.DataSet`.<br /><br /> È possibile usare un'attività Script per accedere all'oggetto `System.Data.DataSet`, come illustrato nell'esempio seguente.<br /><br /> `Dim dt As Data.DataTable` <br /> `Dim ds As Data.DataSet = CType(Dts.Variables("Recordset").Value, DataSet)` <br /> `dt = ds.Tables(0)`|  
|XML|`String`|`String`|  
|XML|`Object`|Se nell'attività è usata una gestione connessione nativa, incluse le gestioni connessioni ADO, OLE DB, Excel e ODBC, l'oggetto restituito è un oggetto `MSXML6.IXMLDOMDocument`.<br /><br /> Se l'attività usa una gestione connessione gestita, ad esempio la gestione connessione [!INCLUDE[vstecado](../includes/vstecado-md.md)], l'oggetto restituito è un oggetto `System.Xml.XmlDocument`.|  
  
 La variabile può essere definita nell'ambito dell'attività Esegui SQL o nell'ambito del pacchetto. Se la variabile viene definita nell'ambito del pacchetto, il set di risultati sarà disponibile per altre attività e contenitori all'interno del pacchetto e per altri pacchetti eseguiti dalle attività Esegui pacchetto o Esegui pacchetto DTS 2000.  
  
 Quando si esegue il mapping di una variabile a un set di risultati di tipo **Riga singola**, i valori non costituiti da stringhe restituiti dall'istruzione SQL vengono convertiti in stringhe se sussistono le condizioni seguenti:  
  
-   La proprietà **TypeConversionMode** è impostata su true. Il valore della proprietà viene impostato nella finestra Proprietà o tramite l' **Editor attività Esegui SQL**.  
  
-   La conversione non comporterà il troncamento dei dati.  
  
 Per informazioni sul caricamento di un set di risultati in una variabile, vedere [Mapping di set di risultati a variabili in un'attività Esegui SQL](control-flow/execute-sql-task.md).  
  
##  <a name="Configure_result_sets"></a>Configurazione dei set di risultati nell'attività Esegui SQL  
 Per altre informazioni sulle proprietà dei set di risultati che è possibile impostare in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Editor attività Esegui SQL &#40;pagina del set di risultati&#41;](../../2014/integration-services/execute-sql-task-editor-result-set-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un'attività o di un contenitore](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 [Mapping di set di risultati a variabili in un'attività Esegui SQL](control-flow/execute-sql-task.md)  
  
## <a name="related-content"></a>Contenuto correlato  
  
-   Esempio CodePlex sull' [esecuzione di parametri SQL e set di risultati](https://go.microsoft.com/fwlink/?LinkId=157863)sul sito Web msftisprodsamples.codeplex.com  
  
  
