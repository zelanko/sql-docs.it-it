---
title: Implementare una ricerca in modalità No Cache o Partial Cache | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Lookup transformation
- match exactly [Integration Services]
- lookups [Integration Services]
- exact matches [Integration Services]
ms.assetid: 01b7fbca-5181-4d47-9f75-7f25af6b40d2
author: janinezhang
ms.author: janinez
ms.openlocfilehash: c0b4286836f3ed7060eceee1b1201670574123cc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944281"
---
# <a name="implement-a-lookup-in-no-cache-or-partial-cache-mode"></a>Implementazione di una ricerca in modalità No Cache o Partial Cache

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  È possibile configurare la trasformazione Ricerca per utilizzare la modalità Partial Cache o No Cache:  
  
-   Partial Cache  
  
     Le righe con le voci corrispondenti nel set di dati di riferimento e, facoltativamente, le righe senza voci corrispondenti nel set di dati sono archiviate nella cache. Quando viene superata la dimensione massima consentita per la memoria della cache, la trasformazione Ricerca rimuove automaticamente dalla cache le righe utilizzate meno frequentemente.  
  
-   No Cache  
  
     Non sono stati caricati dati in cache.  
  
 Se viene selezionata la modalità Partial Cache o No Cache, utilizzare una Gestione connessione OLE DB per collegarsi al set di dati di riferimento. Il set di dati di riferimento viene generato utilizzando una tabella, una visualizzazione o una query SQL durante l'esecuzione della trasformazione Ricerca  
  
### <a name="to-implement-a-lookup-transformation-in-no-cache-or-partial-cache-mode"></a>Per implementare una trasformazione Ricerca in modalità No Cache o Partial Cache  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] contenente il pacchetto che si desidera utilizzare.  
  
2.  Nella scheda **Flusso di dati** aggiungere una trasformazione Ricerca.  
  
3.  Connettere la trasformazione Ricerca al flusso di dati trascinando un connettore da un'origine o una trasformazione precedente alla trasformazione Ricerca.  
  
    > [!NOTE]  
    >  Una trasformazione Ricerca configurata per l'utilizzo in modalità No cache può non essere convalidata se si connette a un file flat che contiene un campo di tipo data vuoto. La convalida della trasformazione varia a seconda che per la gestione connessione relativa al file flat sia configurato o meno il mantenimento dei valori Null. Per assicurarsi che la Trasformazione Ricerca venga convalidata, in **Editor origine file flat**nella **pagina Gestione connessione**selezionare l'opzione **Mantieni i valori Null dell'origine come valori Null nel flusso di dati** .  
  
4.  Fare doppio clic sulla trasformazione di origine o precedente per configurare il componente.  
  
5.  Fare doppio clic sulla trasformazione Ricerca e quindi, in **Editor trasformazione Ricerca**, nella pagina **Generale** , selezionare **Partial cache** o **No cache**.  
  
6.  Dall'elenco **Specificare come gestire le righe senza voci corrispondenti** selezionare un'opzione di gestione degli errori.  
  
7.  Nella pagina **Connessione** selezionare una gestione connessione dall'elenco **Gestione connessione OLE DB** o fare clic su **Nuova** per creare una nuova gestione connessione. Per altre informazioni, vedere [Gestione connessione OLE DB](../../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
8.  Eseguire una delle operazioni seguenti:  
  
    -   Fare clic su **Usa una tabella o una vista**e quindi selezionare una tabella o una vista oppure fare clic su **Nuova** per creare una tabella o una vista.  
  
    -   Fare clic su **Usa i risultati di una query SQL**e quindi compilare una query nella finestra **Comando SQL** .  
  
         oppure  
  
         Fare clic su **Compila query** per compilare una query usando gli strumenti grafici forniti da **Generatore query** .  
  
         oppure  
  
         Fare clic su **Sfoglia** per importare un'istruzione SQL da un file.  
  
     Per convalidare la query SQL, fare clic su **Analizza query**.  
  
     Per visualizzare un campione di dati, fare clic su **Anteprima**.  
  
9. Fare clic sulla pagina **Colonne** e trascinare almeno una colonna dall'elenco **Colonne di input disponibili** a una colonna dell'elenco **Colonne di ricerca disponibili** .  
  
    > [!NOTE]  
    >  La trasformazione Ricerca esegue automaticamente il mapping delle colonne con lo stesso nome e lo stesso tipo di dati.  
  
    > [!NOTE]  
    >  È possibile eseguire il mapping solo di colonne con tipi di dati corrispondenti. Per altre informazioni, vedere [Tipi di dati di Integration Services](../../../integration-services/data-flow/integration-services-data-types.md).  
  
10. Includere colonne di ricerca nell'output eseguendo le operazioni seguenti:  
  
    1.  Selezionare le colonne desiderate dall'elenco **Colonne di ricerca disponibili** .  
  
    2.  Nell'elenco **Operazione di ricerca** specificare se i valori dalle colonne di ricerca sostituiscono quelli nella colonna di input o vengono scritti in una nuova colonna.  
  
11. Se al passaggio 5 è stato selezionato **Partial cache** , nella pagina **Avanzate** impostare le opzioni della cache seguenti:  
  
    -   Dall'elenco **Dimensioni cache (32 bit)** selezionare le dimensioni cache per gli ambienti a 32 bit.  
  
    -   Dall'elenco **Dimensioni cache (64 bit)** selezionare le dimensioni cache per gli ambienti a 64 bit.  
  
    -   Per memorizzare nella cache le righe senza voci corrispondenti nel riferimento, selezionare **Attiva cache per righe senza voci corrispondenti**.  
  
    -   Dall'elenco **Allocazione dalla cache** selezionare la percentuale della cache da usare per archiviare le righe senza voci corrispondenti.  
  
12. Per modificare l'istruzione SQL che genera il set di dati di riferimento, selezionare **Modifica istruzione SQL**e modificare l'istruzione SQL visualizzata nella casella di testo.  
  
     Se l'istruzione include parametri, fare clic su **Parametri** per eseguire il mapping dei parametri alle colonne di input.  
  
    > [!NOTE]  
    >  L'istruzione SQL facoltativa specificata in questa pagina sostituisce il nome della tabella specificato nella pagina **Connessione** di **Editor trasformazione Ricerca**in quanto ha la priorità su di esso.  
  
13. Per configurare l'output degli errori, fare clic sulla pagina **Output errori** e impostare le opzioni di gestione degli errori. Per altre informazioni, vedere [Editor trasformazione Ricerca &#40;pagina Output degli errori&#41;](../../../integration-services/data-flow/transformations/lookup-transformation-editor-error-output-page.md).  
  
14. Fare clic su **OK** per salvare le modifiche alla trasformazione Ricerca e quindi eseguire il pacchetto.  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
