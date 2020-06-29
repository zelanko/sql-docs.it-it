---
title: Trasformazione Mappa caratteri | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.charactertrans.f1
helpviewer_keywords:
- mutually exclusive mapping [Integration Services]
- mapping data [Integration Services]
- string functions
- Character Map transformation [Integration Services]
ms.assetid: e0f50eb6-b893-400f-bb8c-fb3072cc2620
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 00c66af1d609e2e1730be8b7647bdc881d129caf
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85431018"
---
# <a name="character-map-transformation"></a>Trasformazione Mappa caratteri
  La trasformazione Mappa caratteri consente di applicare funzioni per i valori stringa, quale la conversione da minuscolo a maiuscolo, a dati di tipo carattere. È possibile utilizzare questa trasformazione solo su dati di colonna con un tipo di dati string.  
  
 La trasformazione Mappa caratteri consente di convertire dati di colonna sul posto oppure di aggiungere una colonna all'output della trasformazione e inserire i dati convertiti nella nuova colonna. È possibile applicare vari set di operazioni di mapping alla stessa colonna di input e inserire i risultati in colonne diverse. È ad esempio possibile convertire la stessa colonna in maiuscolo e minuscolo, quindi inserire i risultati in due colonne diverse.  
  
 In alcune circostanze il mapping può causare il troncamento dei dati. Può verificarsi un troncamento ad esempio in caso di mapping da caratteri a un byte a caratteri con rappresentazione MBCS (Multibyte Character Set). La trasformazione Mappa caratteri include un output degli errori, che può essere utilizzato per dirigere i dati troncati a un output distinto. Per altre informazioni, vedere [Gestione degli errori nei dati](../error-handling-in-data.md).  
  
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
|Lettere minuscole|Converte i caratteri in minuscolo.|  
|Cinese semplificato|Esegue il mapping da caratteri in cinese tradizionale a caratteri in cinese semplificato.|  
|Cinese tradizionale|Esegue il mapping da caratteri in cinese semplificato a caratteri in cinese tradizionale.|  
|Maiuscolo|Converte i caratteri in maiuscolo.|  
  
## <a name="mutually-exclusive-mapping-operations"></a>Operazioni di mapping che si escludono a vicenda  
 In una stessa trasformazione è possibile eseguire più di un'operazione. Esistono tuttavia operazioni di mapping che si escludono a vicenda. Nella tabella seguente sono elencate le restrizioni applicate quando vengono eseguite più operazioni sulla stessa colonna. Le operazioni nelle colonne Operazione A e Operazione B si escludono a vicenda.  
  
|Operazione A|Operazione B|  
|-----------------|-----------------|  
|Lettere minuscole|Maiuscolo|  
|Hiragana|Katakana|  
|Metà larghezza|Larghezza intera|  
|Cinese tradizionale|Cinese semplificato|  
|Lettere minuscole|Hiragana, katakana, metà larghezza, larghezza intera|  
|Maiuscolo|Hiragana, katakana, metà larghezza, larghezza intera|  
  
## <a name="configuration-of-the-character-map-transformation"></a>Configurazione della trasformazione Mappa caratteri  
 Per configurare la trasformazione Mappa caratteri, procedere nel modo seguente:  
  
-   Specificare le colonne da convertire.  
  
-   Specificare le operazioni da applicare a ogni colonna.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor trasformazione Mappa caratteri** , vedere [Editor trasformazione Mappa caratteri](../../character-map-transformation-editor.md).  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../../common-properties.md)  
  
-   [proprietà personalizzate della trasformazione](transformation-custom-properties.md)  
  
 Per ulteriori informazioni sulle procedure per l'impostazione delle proprietà, fare clic su uno degli argomenti seguenti:  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md)  
  
-   [Ordinamento dei dati per le trasformazioni Unione e Merge Join](sort-data-for-the-merge-and-merge-join-transformations.md)  
  
  
