---
title: Proprietà personalizzate dell'origine CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 744e9357-94a9-4202-abe8-1d3d202697e9
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b82c9db104783e4a725964a2d781d4f3ded40aeb
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58289707"
---
# <a name="cdc-source-custom-properties"></a>Proprietà personalizzate dell'origine CDC
  Nella tabella seguente vengono descritte le proprietà personalizzate dell'origine CDC. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|Connessione|ADO.Net Connection|Connessione ADO.NET al database CDC di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per l'accesso alle tabelle delle modifiche.|  
|StateVariable|String|Variabile del pacchetto di stringhe SSIS che gestisce lo stato CDC dell'esecuzione CDC corrente.|  
|CdcProcessingMode|Integer (enumerazione)|Questa modalità determina il modo in cui viene gestita l'elaborazione. Le opzioni possibili sono **All**, **All with old values**, **Net**, **Net with update mask**e **Net with merge**.<br /><br /> Le modalità il cui nome inizia con All restituiscono tutte le modifiche, mentre quelle il cui nome inizia con Net restituiscono solo le modifiche delta.<br /><br /> Le tabelle senza una chiave primaria possono accettare solo i valori ALL.<br /><br /> **Net with Update Mask** consente di aggiungere colonne booleane con il modello di nome **__$\<column-name>\__Changed**, che indica le colonne modificate nella riga delle modifiche corrente.<br /><br /> Per altre informazioni sui valori per questa proprietà, vedere [Editor origine CDC &#40;pagina Gestione connessione&#41;](../../integration-services/data-flow/cdc-source-editor-connection-manager-page.md).|  
|CaptureInstance|String|Nome dell'istanza di acquisizione CDC con la tabella CDC da leggere. Una tabella di origine acquisita può contenere una o due istanze acquisite per gestire la transizione senza problemi della definizione di tabella mediante modifiche dello schema. Se per la tabella di origine in corso di acquisizione sono definite più istanze di acquisizione, selezionare l'istanza di acquisizione che si desidera utilizzare a questo punto. Il nome dell'istanza di acquisizione predefinito per una tabella [schema].[tabella] è \<schema_\<tabella, ma i nomi delle istanze di acquisizione effettivi in uso possono essere diversi. La tabella effettiva da cui viene eseguita la lettura è la tabella CDC **cdc .\<istanza-acquisizione>_CT**.|  
|ReprocessingIndicator|Boolean|Valore che specifica se aggiungere la colonna **__$reprocessing** . Questa colonna di output speciale consente allo sviluppatore di SSIS di gestire gli errori di consistenza in modo diverso quando si utilizza l'intervallo di elaborazione iniziale.<br /><br /> Se il valore è **true**, viene aggiunta la colonna  **__$reprocessing** .<br /><br /> Il valore di questa colonna è **true** quando l'intervallo di elaborazione CDC si sovrappone all'intervallo di elaborazione iniziale (intervallo di LSN che corrisponde al periodo di caricamento iniziale) o quando un intervallo di elaborazione CDC viene rielaborato a causa di un errore in un'esecuzione precedente. Questa colonna indicatore consente agli sviluppatori di SSIS di gestire gli errori in modo diverso durante la rielaborazione delle modifiche. Azioni quali l'eliminazione di una riga non esistente e l'inserimento non riuscito su una chiave duplicata, ad esempio, possono essere ignorate.<br /><br /> Il valore predefinito è **false**.|  
|CommandTimeout|Integer|Questo valore indica il timeout (in secondi) da usare quando si comunica con il database di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Questo valore viene utilizzato quando il tempo di risposta dal database è molto lento e il valore predefinito (30 secondi) non è sufficiente.|  
  
 Per altre informazioni sull'origine CDC, vedere [Origine CDC](../../integration-services/data-flow/cdc-source.md).  
  
  
