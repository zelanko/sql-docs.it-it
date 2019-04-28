---
title: Creare una dimensione di tipo valuta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], currency
- currency [Analysis Services]
- converting currency
- currency dimensions [Analysis Services]
ms.assetid: b1f037d1-ce47-4e47-a1c2-5ec9e781cff6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dc9b89f4c1d3a1a44d5a568a47d16276639bb4cf
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726735"
---
# <a name="create-a-currency-type-dimension"></a>Creare una dimensione di tipo Valuta
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] una dimensione di tipo Valuta è una dimensione i cui attributi rappresentano un elenco di valute per la generazione di report finanziari.  
  
 Una dimensione di tipo Valuta consente di aggiungere funzionalità di conversione di valuta a un cubo in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per aggiungere funzionalità di conversione di valuta a un cubo, è possibile utilizzare la Configurazione guidata funzionalità di Business Intelligence per definire un comando script MDX (Multidimensional Expressions) che consenta di convertire le misure di valuta in valori appropriati per le impostazioni locali dell'applicazione client. Per creare tale script MDX, nella Configurazione guidata funzionalità di Business Intelligence sono necessarie le informazioni seguenti:  
  
-   Una dimensione di tipo Valuta che rappresenta le valute di origine, ovvero la dimensione di tipo Valuta di origine.  
  
-   Un gruppo di misure che rappresenta i tassi di cambio utilizzati.  
  
 In base a tali informazioni, tramite la Configurazione guidata funzionalità di Business Intelligence verrà automaticamente progettato un processo di conversione di valuta che identifica la dimensione di tipo Valuta di destinazione appropriata, ovvero la dimensione di tipo Valuta che rappresenta le valute di destinazione. In base al numero di conversioni di valuta necessarie alla soluzione di Business Intelligence, tramite la Configurazione guidata funzionalità di Business Intelligence è possibile definire più dimensioni di tipo Valuta di destinazione. Per altre informazioni sulla definizione di conversioni di valuta, vedere [Conversioni di valuta &#40;Analysis Services&#41;](../currency-conversions-analysis-services.md).  
  
 Per identificare una dimensione come dimensione di tipo Valuta, impostare la proprietà `Type` della dimensione su `Currency`.  
  
## <a name="dimension-structure"></a>Struttura dimensione  
 Una dimensione di tipo Valuta contiene almeno un attributo chiave che identifica singole valute nella tabella della dimensione per la dimensione di tipo Valuta. Il valore dell'attributo chiave è diverso nelle dimensioni di tipo Valuta di origine e di destinazione:  
  
-   Per identificare un attributo come attributo chiave di una dimensione di tipo Valuta di origine, impostare la proprietà `Type` dell'attributo su `CurrencySource`.  
  
-   Per identificare un attributo come dimensione di tipo Valuta di destinazione, impostare la proprietà `Type` dell'attributo su `CurrencyDestination`.  
  
 Ai fini della generazione di report, sia la dimensione di tipo Valuta di origine che quella di destinazione possono facoltativamente includere gli attributi seguenti:  
  
-   Un attributo Nome valuta.  
  
     Per identificare un attributo come attributo Nome valuta, impostare la proprietà `Type` dell'attributo su `CurrencyName`.  
  
-   Un attributo Origine valuta.  
  
     Per identificare un attributo come attributo Origine valuta, impostare la proprietà `Type` dell'attributo su `CurrencySource`.  
  
-   Un codice ISO (International Standards Organization) valuta.  
  
     Per identificare un attributo come attributo Codice ISO valuta, impostare la proprietà `Type` dell'attributo su `CurrencyIsoCode`.  
  
 Per altre informazioni sui tipi di attributi, vedere [Configurare tipi di attributi](attribute-properties-configure-attribute-types.md).  
  
## <a name="defining-account-intelligence-with-the-business-intelligence-wizard"></a>Definizione di funzionalità di Business Intelligence per la contabilità tramite la Configurazione guidata funzionalità di Business Intelligence  
 Dopo avere definito una dimensione di tipo Conti e avere aggiunto tale dimensione a un cubo, è possibile utilizzare la Configurazione guidata funzionalità di Business Intelligence per aggiungere funzionalità di Business Intelligence per la contabilità, ad esempio funzionalità di identificazione e mapping dei tipi di conto, alla dimensione. Per altre informazioni, vedere [Aggiungere funzionalità di Business Intelligence per la contabilità a una dimensione](bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi e gerarchie di attributi](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Guida sensibile al contesto della Configurazione guidata funzionalità di Business Intelligence](../business-intelligence-wizard-f1-help.md)   
 [Tipi di dimensioni](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
