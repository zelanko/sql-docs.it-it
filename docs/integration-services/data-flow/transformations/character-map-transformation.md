---
title: Trasformazione Mappa caratteri | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.charactertrans.f1
- sql13.dts.designer.charactermaptransformation.f1
helpviewer_keywords:
- mutually exclusive mapping [Integration Services]
- mapping data [Integration Services]
- string functions
- Character Map transformation [Integration Services]
ms.assetid: e0f50eb6-b893-400f-bb8c-fb3072cc2620
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: cb26cf898282273ea94b07c7d3b6c618d476a35b
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58273003"
---
# <a name="character-map-transformation"></a>Trasformazione Mappa caratteri
  La trasformazione Mappa caratteri consente di applicare funzioni per i valori stringa, quale la conversione da minuscolo a maiuscolo, a dati di tipo carattere. È possibile utilizzare questa trasformazione solo su dati di colonna con un tipo di dati string.  
  
 La trasformazione Mappa caratteri consente di convertire dati di colonna sul posto oppure di aggiungere una colonna all'output della trasformazione e inserire i dati convertiti nella nuova colonna. È possibile applicare vari set di operazioni di mapping alla stessa colonna di input e inserire i risultati in colonne diverse. È ad esempio possibile convertire la stessa colonna in maiuscolo e minuscolo, quindi inserire i risultati in due colonne diverse.  
  
 In alcune circostanze il mapping può causare il troncamento dei dati. Può verificarsi un troncamento ad esempio in caso di mapping da caratteri a un byte a caratteri con rappresentazione MBCS (Multibyte Character Set). La trasformazione Mappa caratteri include un output degli errori, che può essere utilizzato per dirigere i dati troncati a un output distinto. Per altre informazioni, vedere [Gestione degli errori nei dati](../../../integration-services/data-flow/error-handling-in-data.md).  
  
 Questa trasformazione include un input, un output e un output degli errori.  
  
## <a name="mapping-operations"></a>Operazioni di mapping  
 Nella tabella seguente vengono descritte le operazioni di mapping supportate dalla trasformazione Mappa caratteri.  
  
|Operazione|Descrizione|  
|---------------|-----------------|  
|Inversione byte|Inverte l'ordine dei byte.|  
|Larghezza intera|Esegue il mapping da caratteri a metà larghezza a caratteri a larghezza intera.|  
|Metà larghezza|Esegue il mapping da caratteri a larghezza intera a caratteri a metà larghezza.|  
|Hiragana|Esegue il mapping da caratteri Katakana a caratteri Hiragana.|  
|Katakana|Esegue il mapping da caratteri Hiragana a caratteri Katakana.|  
|Conversione da maiuscole a minuscole (e viceversa) basata sulla lingua|Applica la conversione da maiuscole a minuscole (e viceversa) basata sulla lingua anziché le regole di sistema. La conversione da maiuscole a minuscole (e viceversa) basata sulla lingua fa riferimento a una funzionalità disponibile nell'API Win32 per il mapping Unicode semplice tra maiuscole e minuscole per il turco e altre impostazioni locali.|  
|Minuscolo|Converte i caratteri in minuscolo.|  
|Cinese semplificato|Esegue il mapping da caratteri in cinese tradizionale a caratteri in cinese semplificato.|  
|Cinese tradizionale|Esegue il mapping da caratteri in cinese semplificato a caratteri in cinese tradizionale.|  
|Maiuscolo|Converte i caratteri in maiuscolo.|  
  
## <a name="mutually-exclusive-mapping-operations"></a>Operazioni di mapping che si escludono a vicenda  
 In una stessa trasformazione è possibile eseguire più di un'operazione. Esistono tuttavia operazioni di mapping che si escludono a vicenda. Nella tabella seguente sono elencate le restrizioni applicate quando vengono eseguite più operazioni sulla stessa colonna. Le operazioni nelle colonne Operazione A e Operazione B si escludono a vicenda.  
  
|Operazione A|Operazione B|  
|-----------------|-----------------|  
|Minuscolo|Maiuscolo|  
|Hiragana|Katakana|  
|Metà larghezza|Larghezza intera|  
|Cinese tradizionale|Cinese semplificato|  
|Minuscolo|Hiragana, katakana, metà larghezza, larghezza intera|  
|Maiuscolo|Hiragana, katakana, metà larghezza, larghezza intera|  
  
## <a name="configuration-of-the-character-map-transformation"></a>Configurazione della trasformazione Mappa caratteri  
 Per configurare la trasformazione Mappa caratteri, procedere nel modo seguente:  
  
-   Specificare le colonne da convertire.  
  
-   Specificare le operazioni da applicare a ogni colonna.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Per ulteriori informazioni sulle procedure per l'impostazione delle proprietà, fare clic su uno degli argomenti seguenti:  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordinare i dati per le trasformazioni Unione e Merge Join](../../../integration-services/data-flow/transformations/sort-data-for-the-merge-and-merge-join-transformations.md)  
  
## <a name="character-map-transformation-editor"></a>Editor trasformazione Mappa caratteri
  Usare la finestra di dialogo **Editor trasformazione Mappa caratteri** per selezionare le funzioni per i valori stringa da applicare ai dati di colonna e per specificare se il mapping è una modifica sul posto o viene aggiunto come nuova colonna.  
  
### <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Utilizzare le caselle di controllo per selezionare le colonne da trasformare utilizzando le funzioni per i valori stringa. Le selezioni verranno visualizzate nella tabella sottostante.  
  
 **Colonna di input**  
 Consente di visualizzare le colonne di input selezionate nella tabella precedente. È inoltre possibile modificare o rimuovere una selezione utilizzando l'elenco di colonne di input disponibili.  
  
 **Destinazione**  
 Consente di specificare se salvare i risultati delle operazioni di stringa sul posto, utilizzando la colonna esistente, o se salvare i dati modificati come nuova colonna.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|Nuova colonna|Consente di salvare i dati in una nuova colonna. Assegnare il nome alla colonna in **Alias di output**.|  
|Modifica sul posto|Consente di salvare i dati modificati nella colonna esistente.|  
  
 **Operazione**  
 Consente di selezionare nell'elenco le funzioni per i valori stringa da applicare ai dati della colonna.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|Minuscolo|Consente di convertire la stringa in caratteri minuscoli.|  
|Maiuscolo|Consente di convertire la stringa in caratteri maiuscoli.|  
|Inversione byte|Consente di eseguire la conversione invertendo l'ordine dei byte.|  
|Hiragana|Consente di convertire i caratteri giapponesi katakana in caratteri hiragana.|  
|Katakana|Consente di convertire i caratteri giapponesi hiragana in caratteri katakana.|  
|Metà larghezza|Consente di convertire i caratteri a larghezza intera in caratteri a metà larghezza.|  
|Larghezza intera|Consente di convertire i caratteri a metà larghezza in caratteri a larghezza intera.|  
|Conversione da maiuscole a minuscole (e viceversa) basata sulla lingua|Consente di applicare le regole di conversione da maiuscole a minuscole (e viceversa) basata sulla lingua, ovvero il mapping Unicode semplice tra maiuscole e minuscole per il turco e altre impostazioni locali, al posto delle regole di sistema.|  
|Cinese semplificato|Consente di convertire i caratteri in cinese tradizionale in caratteri in cinese semplificato.|  
|Cinese tradizionale|Consente di convertire i caratteri in cinese semplificato in caratteri in cinese tradizionale.|  
  
 **Alias di output**  
 Consente di digitare un alias per ogni colonna di output. L'impostazione predefinita è **Copia di** seguita dal nome della colonna di input.  È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
 **Configura output errori**  
 Usare la finestra di dialogo [Configura output errori](https://msdn.microsoft.com/library/5f8da390-fab5-44f8-b268-d8fa313ce4b9) per specificare le opzioni di gestione degli errori per la trasformazione corrente.  
  
  
