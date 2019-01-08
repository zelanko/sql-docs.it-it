---
title: L'oggetto campo | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Field object [ADO]
ms.assetid: 7d1c4ad5-4be3-42ab-b516-e7133ca300bc
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e152c3147ab7c316494c6891424c0a7c8173f002
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516539"
---
# <a name="the-field-object"></a>Oggetto Field
Ciascuna **campo** oggetto in genere corrisponde a una colonna in una tabella di database. Tuttavia, un **campo** può inoltre rappresentare un puntatore a un'altra **Recordset**, chiamato un capitolo. Eccezioni, ad esempio le colonne a capitoli, verranno trattate più avanti in questa Guida.  
  
 Usare la **valore** proprietà di **campo** oggetti da impostare o restituire i dati per il record corrente. A seconda della funzionalità espone il provider, alcune raccolte, metodi o proprietà di un **campo** oggetto potrebbe non essere disponibile.  
  
 Con le raccolte, i metodi e proprietà di un **campo** dell'oggetto, è possibile eseguire le operazioni seguenti:  
  
-   Restituire il nome di un campo utilizzando il **nome** proprietà.  
  
-   Visualizzare o modificare i dati nel campo utilizzando il **valore** proprietà. **Valore** è la proprietà predefinita di **campo** oggetto.  
  
-   Restituire le caratteristiche di base di un campo utilizzando il **tipo**, **precisione**, e **NumericScale** proprietà.  
  
-   Restituire la dimensione dichiarata di un campo utilizzando il **DefinedSize** proprietà.  
  
-   Restituire la dimensione effettiva dei dati in un determinato campo utilizzando il **ActualSize** proprietà.  
  
-   Determinare i tipi di funzionalità sono supportati per un determinato campo tramite il **attributi** proprietà e **proprietà** raccolta.  
  
-   Modificare i valori dei campi che contengono dati long carattere o binari long usando il **AppendChunk** e **GetChunk** metodi.  
  
 Risolvere le differenze tra i valori dei campi durante l'aggiornamento in batch usando il **OriginalValue** e **UnderlyingValue** proprietà, se il provider supporta gli aggiornamenti in batch.  
  
## <a name="describing-a-field"></a>Che descrive un campo  
 Gli argomenti che seguono verranno illustrano le proprietà del [campo](../../../ado/reference/ado-api/field-object.md) oggetti che rappresentano le informazioni che descrivono le **campo** oggetto stesso, vale a dire, i metadati relativi al campo. Queste informazioni possono essere utilizzate per determinare le sullo schema del **Recordset**. Queste proprietà includono **tipo**, **DefinedSize** e **ActualSize**, **nome**, e **NumericScale**e **precisione**.  
  
### <a name="discovering-the-data-type"></a>Individuare il tipo di dati  
 Il **tipo** proprietà indica il tipo di dati del campo. Il tipo di dati costanti enumerate supportati da ADO sono descritti in [DataTypeEnum](../../../ado/reference/ado-api/datatypeenum.md) nel *riferimento per programmatori ADO*.  
  
 Ad esempio tipi numerici di virgola mobile **adNumeric**, è possibile ottenere altre informazioni. Il **NumericScale** proprietà indica il numero di cifre a destra del separatore decimale da utilizzare per rappresentare i valori per il **campo**. Il **precisione** proprietà specifica il numero massimo di cifre utilizzate per rappresentare i valori per il **campo**.  
  
### <a name="determining-field-size"></a>Determinazione della dimensione del campo  
 Usare la **DefinedSize** proprietà per determinare la capacità di dati di un **campo** oggetto.  
  
 Usare la **ActualSize** proprietà per restituire la lunghezza effettiva di un **campo** valore dell'oggetto. Per tutti i campi, il **ActualSize** proprietà è di sola lettura. Se ADO non è possibile determinare la lunghezza del **campo** valore dell'oggetto, il **ActualSize** restituisce proprietà **adUnknown**.  
  
 Il **DefinedSize** e **ActualSize** proprietà hanno scopi diversi. Si consideri, ad esempio, un **campo** oggetto con un tipo dichiarato del **adVarChar** e un **DefinedSize** valore della proprietà di 50, che contiene un singolo carattere. Il **ActualSize** valore restituito della proprietà è la lunghezza in byte del carattere singolo.  
  
### <a name="determining-field-contents"></a>Determinazione di contenuto del campo  
 L'identificatore della colonna dall'origine dati è rappresentato dal **Name** proprietà delle **campo**. Il **valore** proprietà delle **campo** oggetto restituisce o imposta il contenuto effettivo dei dati del campo. Questa è la proprietà predefinita.  
  
 Per modificare i dati in un campo, impostare il **valore** proprietà è uguale a un nuovo valore del tipo corretto. Il tipo di cursore debba supportare gli aggiornamenti per modificare il contenuto di un campo. Convalida del database non viene eseguita qui in modalità batch, pertanto sarà necessario verificare la presenza di errori quando si chiama **UpdateBatch** in questo caso. Alcuni provider supportano anche l'oggetto ADO **campo** dell'oggetto **UnderlyingValue** e **OriginalValue** le proprietà per facilitare la risoluzione dei conflitti quando si prova a eseguire gli aggiornamenti batch. Per informazioni dettagliate su come risolvere questi conflitti, vedere [modifica dei dati](../../../ado/guide/data/editing-data.md).  
  
> [!NOTE]
>  **Recordset Field** valori non possono essere impostati caso di aggiunta di nuove **campi** a un **Recordset**. Piuttosto, nuove **i campi** può essere aggiunto a un oggetto chiuso **Recordset**. L'oggetto **Recordset** devono essere aperti e solo allora possono essere assegnati i valori queste **campi**.  
  
### <a name="getting-more-field-information"></a>Ottenere altre informazioni sui campi  
 Gli oggetti ADO presentano due tipi di proprietà: predefinito e dinamico. A questo punto, solo le proprietà predefinite del **campo** oggetto sono stati trattati.  
  
 Proprietà predefinite sono le proprietà implementate in ADO e immediatamente disponibili per qualsiasi nuovo oggetto, tramite il `MyObject.Property` sintassi. Non sono visualizzate come **proprietà** gli oggetti in un oggetto **proprietà** raccolta.  
  
 Proprietà dinamiche sono definite dal provider di dati sottostanti e vengono visualizzati nei **proprietà** raccolta per l'oggetto ADO appropriato. Ad esempio, una proprietà specifica del provider può indicare se un **Recordset** oggetto supporta le transazioni o l'aggiornamento. Queste proprietà aggiuntive verranno visualizzato come **proprietà** gli oggetti in quanto **Recordset** dell'oggetto **proprietà** raccolta. Proprietà dinamiche è possibile fare riferimento solo tramite la raccolta, usando la sintassi `MyObject.Properties(0)` o `MyObject.Properties("Name")`.  
  
 Non è possibile eliminare entrambi i tipi di proprietà.  
  
 Dinamico **proprietà** oggetto dispone di quattro proprietà incorporate propri:  
  
-   Il **nome** proprietà è una stringa che identifica la proprietà.  
  
-   Il **tipo** proprietà è un numero intero che specifica il tipo di dati di proprietà.  
  
-   Il **valore** proprietà è una variante che contiene l'impostazione della proprietà. **Valore** è la proprietà predefinita per un **proprietà** oggetto.  
  
-   Il **attributi** proprietà è un **lungo** valore che indica le caratteristiche della proprietà specifiche del provider.  
  
 Il **delle proprietà** raccolta per il **campo** oggetto contiene metadati aggiuntivi sul campo. Il contenuto di questa raccolta varia a seconda del provider. Esempio di codice seguente esamina il **proprietà** raccolta del campione **Recordset** introdotta all'inizio di questa sezione. Viene innanzitutto analizzato il contenuto della raccolta. Questo codice Usa il [il Provider OLE DB per SQL Server](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md), pertanto il **proprietà** raccolta contiene le informazioni rilevanti per tale provider.  
  
```  
'BeginFieldProps  
    Dim objProp As ADODB.Property  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
  
        For Each objProp In objFields(intLoop).Properties  
            Debug.Print vbTab & objProp.Name & " = " & objProp.Value  
        Next objProp  
    Next intLoop  
'EndFieldProps  
```  
  
### <a name="dealing-with-binary-data"></a>Gestione di dati binari  
 Usare la [AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) metodo su un **campo** oggetto per inserirvi i dati caratteri o binari long. In situazioni in cui la memoria di sistema è limitata, è possibile usare la **AppendChunk** metodo per modificare i valori long in parti invece che nel loro complesso.  
  
 Se il **adFldLong** bit nel **attributi** proprietà di un **campo** è impostata su **True**, è possibile usare il  **Metodo AppendChunk** metodo per il campo.  
  
 Il primo **AppendChunk** chiamare su un **campo** oggetto scrive i dati e il campo, sovrascrivendo eventuali dati esistenti. Le successive **AppendChunk** chiamate aggiungono ai dati esistenti. Se si Accoda dati a un singolo campo e quindi impostare o leggere il valore di un altro campo nel record corrente, si presume che l'utente abbia terminato di accodamento dei dati nel primo campo. Se si chiama il **AppendChunk** metodo nel primo campo anche in questo caso, ADO interpreta la chiamata come nuovo **AppendChunk** operazione e sovrascrive i dati esistenti. L'accesso ai campi in altre **Recordset** oggetti che non sono i cloni dei primi **Recordset** oggetto non interromperà **AppendChunk** operazioni.  
  
 Usare la **GetChunk** metodo su un **campo** oggetto per recuperare la parte o tutti i relativi dati caratteri o binari long. In situazioni in cui la memoria di sistema è limitata, è possibile usare la **GetChunk** metodo per modificare i valori long in parti, anziché nella loro interezza.  
  
 I dati che un **GetChunk** chiamata restituisce viene assegnato a *variabile*. Se *dimensioni* è maggiore rispetto ai dati rimanenti, il **GetChunk** metodo restituisce solo i dati rimanenti senza spaziatura interna *variabile* con gli spazi vuoti. Se il campo è vuoto, il **GetChunk** metodo restituisce un valore null.  
  
 Ogni successivo **GetChunk** chiamata recupera i dati a partire dalla posizione in cui il precedente **GetChunk** chiamata è stata interrotta. Tuttavia, se si recuperano dati da un campo e quindi impostare o leggere il valore di un altro campo nel record corrente, ADO presuppone di che aver completato il recupero dei dati dal primo campo. Se si chiama il **GetChunk** metodo nel primo campo anche in questo caso, ADO interpreta la chiamata come nuovo **GetChunk** operazione e inizia la lettura dall'inizio dei dati. L'accesso ai campi in altre **Recordset** oggetti che non sono i cloni dei primi **Recordset** oggetto non interromperà **GetChunk** operazioni.  
  
 Se il **adFldLong** bit nel **attributi** proprietà di un **campo** è impostata su **True**, è possibile usare il **GetChunk**  metodo per il campo.  
  
 Se non è presente nessun record corrente quando si usa il **GetChunk** oppure **AppendChunk** metodo in un **campo** dell'oggetto, verrà generato errore 3021 (Nessun record corrente).  
  
 Per un esempio di uso di questi metodi per manipolare i dati binari, vedere la [metodo AppendChunk](../../../ado/reference/ado-api/appendchunk-method-ado.md) e [metodo GetChunk](../../../ado/reference/ado-api/getchunk-method-ado.md) negli esempi del *riferimento per programmatori ADO*.
