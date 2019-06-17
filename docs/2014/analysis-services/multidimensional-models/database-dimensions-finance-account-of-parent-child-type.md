---
title: Creare un conto finanziario della dimensione di tipo padre-figlio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- dimensions [Analysis Services], account
- account dimensions [Analysis Services]
- adding account intelligence
- account intelligence [Analysis Services]
ms.assetid: 2ba74e81-5b4b-407e-acdf-deb2f6accf0a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 28a7cf6b3a712144daead54d521fb3cc6936c99e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66075915"
---
# <a name="create-a-finance-account-of-parent-child-type-dimension"></a>Creare un conto finanziario della dimensione di tipo padre-figlio
  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] una dimensione di tipo Conto è una dimensione i cui attributi rappresentano un grafico dei conti per la generazione di report finanziari.  
  
 Una dimensione di tipo Conti consente di gestire in modo selettivo le modalità di aggregazione dei conti nel tempo. Una dimensione di tipo Conti consente inoltre di utilizzare un meccanismo standard per risolvere la maggior parte dei problemi di aggregazione non standard che in genere di verificano nelle soluzione di Business Intelligence per la gestione dei dati finanziari. Se non si disponesse di tale meccanismo standard, la risoluzione dei problemi di aggregazione non standard richiederebbe formule personalizzate di rollup, membri calcolati o script MDX (Multidimensional Expressions).  
  
 Per identificare una dimensione come dimensione di tipo Conti, impostare la proprietà `Type` della dimensione su `Accounts`.  
  
## <a name="dimension-structure"></a>Struttura dimensione  
 In una dimensione di tipo Conti sono contenuti almeno due attributi:  
  
-   Un attributo, un attributo chiave che identifica singoli conti nella tabella della dimensione per la dimensione di tipo conti.  
  
-   Un attributo padre di un attributo conto che descrive come gli account vengono disposte in ordine gerarchico nella dimensione di tipo conti.  
  
     Per identificare un attributo come attributo Conto, impostare la proprietà `Type` dell'attributo su `Account` e la proprietà `Usage` su `Parent`.  
  
 Facoltativamente, nelle dimensioni di tipo Conti possono essere contenuti gli attributi seguenti:  
  
-   Un account di tipo di attributo, un attributo che definisce il tipo di account per ogni conto nella dimensione. Viene eseguito il mapping tra i nomi dei membri dell'attributo di tipo Conto e i tipi di conto definiti per il database o il progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e tali nomi indicano la funzione di aggregazione usata da [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per tali conti. È inoltre possibile utilizzare operatori unari o formule personalizzate di rollup per determinare le modalità di aggregazione per gli attributi Conto, ma gli attributi di tipo Conto consentono di applicare in modo semplice un comportamento consistente a un grafico dei conti senza che sia necessario apportare modifiche al database relazionale sottostante.  
  
     Per identificare un attributo di tipo Conto, impostare la proprietà `Type` dell'attributo su `AccountType`.  
  
-   Un nome attributo, un attributo conto che viene usato per la creazione di report. Per identificare un attributo relativo al nome del conto, impostare la proprietà `Type` dell'attributo su `AccountName`.  
  
-   Un account del numero di attributi, un attributo che viene usato per la creazione di report. Per identificare un attributo relativo al numero di conto, impostare la proprietà `Type` dell'attributo su `AccountNumber`.  
  
 Per altre informazioni sui tipi di attributi, vedere [Configurare tipi di attributi](attribute-properties-configure-attribute-types.md).  
  
## <a name="adding-account-intelligence-with-the-business-intelligence-wizard"></a>Aggiunta di funzionalità di Business Intelligence per la contabilità tramite la Configurazione guidata funzionalità di Business Intelligence  
 Dopo avere definito una dimensione di tipo Conti e avere aggiunto tale dimensione a un cubo, è possibile utilizzare la Configurazione guidata funzionalità di Business Intelligence per aggiungere funzionalità di Business Intelligence per la contabilità, ad esempio funzionalità di identificazione e mapping dei tipi di conto, alla dimensione. Per altre informazioni, vedere [Aggiungere funzionalità di Business Intelligence per la contabilità a una dimensione](bi-wizard-add-account-intelligence-to-a-dimension.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Attributi e gerarchie di attributi](../multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md)   
 [Guida sensibile al contesto della Configurazione guidata funzionalità di Business Intelligence](../business-intelligence-wizard-f1-help.md)   
 [Tipi di dimensioni](../multidimensional-models-olap-logical-dimension-objects/database-dimension-properties-types.md)  
  
  
