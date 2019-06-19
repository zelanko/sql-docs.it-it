---
title: Trasformazione Ordinamento | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.sorttrans.f1
- sql13.dts.designer.sorttransformation.f1
helpviewer_keywords:
- Sort transformation
- descending sorts
- ascending sorts
- sorting data [Integration Services]
- multiple sorts
- duplicate data [Integration Services]
ms.assetid: 728c9351-84a8-4a89-be4d-d50d4adc04e0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6a8cb120d8934ca909408de71caf2b2c049bb853
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65725844"
---
# <a name="sort-transformation"></a>Ordinamento - trasformazione

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La trasformazione Ordinamento consente di disporre i dati di input in ordine crescente o decrescente e di copiare i dati ordinati nell'output della trasformazione. A uno stesso input è possibile applicare più ordinamenti, ognuno dei quali è identificato da un numero che ne determina il tipo. La colonna con il numero più basso viene ordinata per prima, quindi viene ordinata quella con il secondo numero più basso e così via. Se ad esempio la colonna di nome **CountryRegion** ha come tipo di ordinamento 1 e la colonna di nome **City** ha come tipo di ordinamento 2, l'output verrà ordinato prima per country/region, quindi per city. Un numero positivo indica che l'ordinamento è crescente, mentre un numero negativo indica che è decrescente. Le colonne che non sono ordinate hanno un tipo di ordinamento 0. Le colonne non selezionate per l'ordinamento vengono copiate automaticamente nell'output della trasformazione insieme alle colonne ordinate.  
  
 La trasformazione Ordinamento include un set di opzioni di confronto che consentono di definire la modalità di gestione dei dati stringa in una colonna. Per altre informazioni, vedere [Comparing String Data](../../../integration-services/data-flow/comparing-string-data.md).  
  
> [!NOTE]  
>  La trasformazione Ordinamento non dispone i GUID nello stesso ordine della clausola ORDER BY in Transact-SQL. La trasformazione Ordinamento dispone i GUID che iniziano con 0-9 prima di quelli che iniziano con A-F, mentre la clausola ORDER BY li ordina in modo diverso, come implementato in [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]. Per altre informazioni, vedere [Clausola ORDER BY &#40;Transact-SQL&#41;](../../../t-sql/queries/select-order-by-clause-transact-sql.md).  
  
 La trasformazione Ordinamento è inoltre in grado di rimuovere le righe duplicate nell'ambito dell'operazione di ordinamento. Sono considerate duplicate le righe che hanno valori di chiave di ordinamento identici. Il valore della chiave di ordinamento viene generato in base alle opzioni utilizzate per il confronto delle stringhe e questo significa che stringhe letterali diverse possono avere gli stessi valori di chiave di ordinamento. La trasformazione identifica come duplicate le righe delle colonne di input che hanno valori di chiave di ordinamento identici, anche se i valori effettivi sono diversi.  
  
 La trasformazione Ordinamento include la proprietà personalizzata **MaximumThreads**, che può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../../../integration-services/expressions/integration-services-ssis-expressions.md), [Utilizzo delle espressioni di proprietà nei pacchetti](../../../integration-services/expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md).  
  
 Questa trasformazione include un input e un output. Non supporta output degli errori.  
  
## <a name="configuration-of-the-sort-transformation"></a>Configurazione della trasformazione Ordinamento  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per altre informazioni su come impostare le proprietà del componente, vedere [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## <a name="related-content"></a>Contenuto correlato  
 Esempio relativo al [componente SSIS personalizzato SortDeDuplicateDelimitedString](https://go.microsoft.com/fwlink/?LinkId=220821)su codeplex.com.  
  
## <a name="sort-transformation-editor"></a>Editor trasformazione Ordinamento
  Utilizzare la finestra di dialogo **Editor trasformazione Ordinamento** per selezionare le colonne da ordinare, impostare il tipo di ordinamento e specificare se rimuovere i duplicati.  
  
### <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Consente di specificare le colonne da ordinare utilizzando le caselle di controllo.  
  
 **Nome**  
 Consente di visualizzare il nome di ogni colonna di input disponibile.  
  
 **Pass-through**  
 Indica se includere la colonna nell'output ordinato.  
  
 **Colonna di input**  
 Consente di selezionare una colonna di input nell'elenco delle colonne di input disponibili per ogni riga. Le selezioni effettuate vengono riflesse nelle selezioni delle caselle di controllo nella tabella **Colonne di input disponibili** .  
  
 **Alias di output**  
 Consente di digitare un alias per ogni colonna di output. Per impostazione predefinita viene suggerito il nome della colonna di input. È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
 **Tipo di ordinamento**  
 Indica se eseguire l'ordinamento in ordine crescente o decrescente.  
  
 **Ordinamento**  
 Indica l'ordine da utilizzare per l'ordinamento delle colonne. È possibile impostare questa opzione in modo manuale per ogni colonna.  
  
 **Flag di confronto**  
 Per altre informazioni sulle opzioni per il confronto di stringhe, vedere [Confronto di dati stringa](../../../integration-services/data-flow/comparing-string-data.md).  
  
 **Rimuovi righe con valori di ordinamento duplicati**  
 Indica se la trasformazione copia le righe duplicate nell'output della trasformazione o se invece crea un'unica voce per tutti i duplicati in base alla stringa specificata nelle opzioni di confronto.  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di dati](../../../integration-services/data-flow/data-flow.md)   
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
  
