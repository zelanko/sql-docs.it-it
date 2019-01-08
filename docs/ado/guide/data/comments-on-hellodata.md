---
title: Commenti su HelloData | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hellodata sample application [ADO]
ms.assetid: a2831d77-7040-4b73-bbae-fe0bf78107ed
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 632703a1f7817986a6bc192006ef079af20cfb08
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527447"
---
# <a name="comments-on-hellodata"></a>Commenti su HelloData
L'applicazione di HelloData illustrata in dettaglio le operazioni di base di una tipica applicazione ADO: introduzione, l'analisi, la modifica e aggiornamento dei dati. Quando si avvia l'applicazione, fare clic sul primo pulsante, **recupera dati**. Verrà eseguita la **GetData** subroutine.  
  
## <a name="getdata"></a>GetData  
 **GetData** inserisce una stringa di connessione valido in una variabile, a livello di modulo *m_sConnStr*. Per altre informazioni sulle stringhe di connessione, vedere [creazione della stringa di connessione](../../../ado/guide/data/creating-a-connection-string.md).  
  
 Assegnare un gestore degli errori utilizzando Visual Basic **OnError** istruzione. Per altre informazioni sulla gestione degli errori in ADO, vedere [Error Handling](../../../ado/guide/data/error-handling.md). Una nuova **connessione** viene creato l'oggetto e il **CursorLocation** è impostata su **adUseClient** poiché nell'esempio di HelloData viene creato un  *Recordset disconnesso*. Ciò significa che non appena i dati sono stati recuperati dall'origine dati, la connessione fisica all'origine dati viene interrotta, ma è possibile proseguire con i dati memorizzati nella cache in locale nel **Recordset** oggetto.  
  
 Dopo aver aperto la connessione, è possibile assegnare una stringa SQL a una variabile (sSQL). Quindi creare un'istanza di una nuova **Recordset** oggetto `m_oRecordset1`. Nella riga successiva del codice, aprire il **Recordset** tramite l'oggetto esistente **connessione**passando `sSQL` come origine della **Recordset**. Consente di ADO in rendendo la determinazione che il codice SQL stringa si hanno superato come origine per il **Recordset** è una definizione di un comando testuale passando **adCmdText** nell'argomento finale per il **Apertura di un Recordset** (metodo). Questa riga imposta anche il **LockType** e **CursorType** associato il **Recordset**.  
  
 La riga successiva del set di codice le **MarshalOptions** uguale alla proprietà **adMarshalModifiedOnly**. **MarshalOptions** indica quali record devono effettuare il marshalling al livello intermedio (o al server Web). Per altre informazioni sul marshalling, vedere la documentazione di COM. Quando si usa **adMarshalModifiedOnly** con un cursore lato client ([CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) = **adUseClient**), solo i record che sono stati modificati di client vengono riscritte al livello intermedio. L'impostazione **MarshalOptions** al **adMarshalModifiedOnly** può migliorare le prestazioni poiché vengono effettuato il marshalling meno righe.  
  
 Successivamente, disconnettere il **Recordset** mediante l'impostazione relativa **ActiveConnection** uguale alla proprietà **Nothing**. Per altre informazioni, vedere la sezione "Disconnettendo e riconnettendo il valore Recordset" nella [aggiornamento e salvataggio permanente dei dati](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Chiudere la connessione all'origine dati ed eliminare definitivamente l'oggetto esistente **connessione** oggetto. Ciò rilascia le risorse che utilizzato.  
  
 Il passaggio finale consiste nell'impostare il **Recordset** come la **DataSource** per il controllo DataGrid Microsoft controllo nel form in modo che è possibile visualizzare i dati dal **Recordset** sul Form.  
  
 Fare clic sul pulsante, secondo **esaminare i dati**. Questo comando esegue la **ExamineData** subroutine.  
  
## <a name="examinedata"></a>ExamineData  
 ExamineData Usa diversi metodi e proprietà del **Recordset** oggetto per visualizzare le informazioni relative ai dati di **Recordset**. Segnala il numero di record usando il **RecordCount** proprietà. Esegue un ciclo tramite il **Recordset** e stampa il valore della **AbsolutePosition** proprietà nella casella di testo visualizzato nel form. Anche all'interno di ciclo, il valore della **segnalibro** proprietà per il terzo record viene inserita in una variabile variant *vBookmark*, per un uso successivo.  
  
 La routine consente di passare direttamente al terzo record utilizzando la variabile segnalibri che archiviato in precedenza. Le chiamate di routine il **WalkFields** subroutine, che consente di scorrere le **campi** raccolta del **Recordset** e Visualizza informazioni dettagliate sui singoli **campo**  nella raccolta.  
  
 Infine **ExamineData** Usa le **filtro** proprietà del **Recordset** nella schermata per solo i record con un **CategoryId** uguale a 2. Il risultato dell'applicazione di questo filtro è immediatamente visibile nella griglia di visualizzazione nel form.  
  
 Per altre informazioni sulle funzionalità visualizzate nel **ExamineData** subroutine, vedere [analisi dei dati](../../../ado/guide/data/examining-data.md).  
  
 Fare quindi clic sul terzo pulsante **la modifica dei dati**. Verrà eseguita la **EditData** subroutine.  
  
## <a name="editdata"></a>EditData  
 Quando il codice avvia il **EditData** subroutine, il **Recordset** ancora viene applicato un filtro **CategoryId** è uguale a 2, in modo che solo gli elementi che soddisfano i criteri di filtro visibile. Viene innanzitutto eseguita una ricerca di **Recordset** e incrementa il prezzo di ogni elemento visibile nel **Recordset** 10 percento. Il valore della **prezzo** campo viene modificato impostando la **valore** proprietà per il campo uguale a una quantità di nuovo, valida.  
  
 Tenere presente che il **Recordset** è disconnesso dall'origine dati. Le modifiche apportate **EditData** vengono apportate solo per la copia dei dati memorizzati nella cache locale. Per altre informazioni, vedere [modifica dei dati](../../../ado/guide/data/editing-data.md).  
  
 Le modifiche non sono pertanto dell'origine dati finché non si sceglie il quarto pulsante **aggiornare i dati**. Verrà eseguita la **UpdateData** subroutine.  
  
## <a name="updatedata"></a>UpdateData  
 UpdateData rimuove prima il filtro viene applicato il **Recordset**. Il codice cancella e reimposta `m_oRecordset1` come il **DataSource** per il controllo DataGrid associato di Microsoft nel form in modo che il non filtrate **Recordset** visualizzato nella griglia.  
  
 Il codice verifica quindi se è possibile spostarsi all'indietro **Recordset** tramite il **supporta** metodo con il **adMovePrevious** argomento.  
  
 La routine passa al primo record usando il **MoveFirst** metodo e visualizza i valori del campo originale e corrente, usando la **OriginalValue** e **valore** proprietà del **campo** oggetto. Queste proprietà, insieme con il **UnderlyingValue** proprietà (non usato in questo esempio), sono descritti in [aggiornamento e salvataggio permanente dei dati](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Successivamente, una nuova **connessione** oggetto viene creato e usato per ristabilire una connessione all'origine dati. Si riconnette il **Recordset** all'origine dei dati impostando la nuova **connessione** come il **ActiveConnection** per il **Recordset**. Per inviare gli aggiornamenti al server, il codice chiama **UpdateBatch** nel **Recordset**.  
  
 Se l'aggiornamento batch ha esito positivo, la variabile a livello di modulo flag `m_flgPriceUpdated`, è impostato su True. Si ricorderà in un secondo momento per pulire tutte le modifiche apportate al database.  
  
 Infine, il codice consente di tornare al primo record nel **Recordset** e visualizza i valori originali e correnti. I valori sono gli stessi dopo la chiamata a **UpdateBatch**.  
  
 Per informazioni dettagliate su come aggiornare i dati, tra cui operazioni da eseguire quando i dati sulle modifiche server durante la **Recordset** viene disconnesso, vedere [aggiornamento e salvataggio permanente dei dati](../../../ado/guide/data/updating-and-persisting-data.md).  
  
## <a name="formunload"></a>Form_Unload  
 Il **Form_Unload** subroutine è importante per diversi motivi. In primo luogo, poiché si tratta di un'applicazione di esempio, Form_Unload pulisce le modifiche apportate al database prima di uscire dall'applicazione. In secondo luogo, il codice viene illustrato come un comando può essere eseguito direttamente da un oggetto aperto **Connection** oggetto tramite il **Execute** (metodo). Infine viene illustrato un esempio di esecuzione di una query non restituiscono righe (una query di aggiornamento) rispetto all'origine dati.
