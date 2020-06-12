---
title: Dimensioni nei modelli multidimensionali | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- OLAP [Analysis Services], dimensions
- dimensions [Analysis Services], about dimensions
- OLAP objects [Analysis Services], dimensions
ms.assetid: 2b62b05c-00fd-4e60-b77f-f707ba83a19b
author: minewiskan
ms.author: owend
ms.openlocfilehash: 85694cfbd86e1c6ada9ff326bc3c212d64274201
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546760"
---
# <a name="dimensions-in-multidimensional-models"></a>Dimensioni nei modelli multidimensionali
  Una dimensione di database è una raccolta di oggetti correlati, denominati attributi, che è possibile utilizzare per offrire informazioni sui dati della tabella dei fatti in uno o più cubi. Gli attributi tipici di una dimensione dei prodotti possono ad esempio essere costituiti da nome del prodotto, categoria di prodotto, linea di prodotti, dimensioni del prodotto e prezzo del prodotto. Tali oggetti sono associati a una o più colonne di una o più tabelle di una vista origine dati Per impostazione predefinita, questi attributi sono visibili come gerarchie di attributo e possono essere utilizzati per acquisire familiarità con le tabelle dei fatti in un cubo. Possono inoltre essere organizzati in gerarchie definite dall'utente che definiscono percorsi di navigazione utili per l'esplorazione dei dati di un cubo.  
  
 I cubi contengono tutte le dimensioni su cui gli utenti basano le analisi dei dati della tabella dei datti. Un'istanza di una dimensione database in un cubo viene denominata dimensione del cubo e fa riferimento a uno o più gruppi di misure nel cubo. Una dimensione del database può essere utilizzata più volte in un cubo. Se una tabella dei fatti include più fatti temporali, ad esempio, è possibile definire una dimensione del cubo separata per facilitare l'analisi di ogni fatto temporale. È tuttavia necessaria una sola dimensione temporale del database e per supportare più dimensioni del cubo basate sul tempo è necessaria una sola tabella del database relazionale di tipo temporale.  
  
> [!NOTE]  
>   Per informazioni sui problemi di prestazioni correlati alla progettazione delle dimensioni, vedere la [Guida alle prestazioni di SQL Server 2008 R2 Analysis Services](https://go.microsoft.com/fwlink/?LinkId=306717).  
  
## <a name="defining-dimensions-attributes-and-hierarchies"></a>Definizione di dimensioni, attributi e gerarchie  
 Il metodo più semplice per definire dimensioni di database e cubi, attributi e gerarchie consiste nell'utilizzare la Creazione guidata cubo per creare dimensioni contemporaneamente alla definizione del cubo. Tramite la Creazione guidata cubo le dimensioni vengono create in base alle tabelle delle dimensioni trovate dalla procedura guidata o specificate dalla vista origine dati utilizzata per il cubo. Nella procedura guidata vengono quindi create le dimensioni del database e vengono aggiunte al nuovo cubo, creando così le dimensioni del cubo.  
  
 Quando si crea un cubo, è inoltre possibile aggiungere al nuovo cubo qualsiasi dimensione già esistente nel database. Tali dimensioni possono essere state definite in precedenza per un altro cubo oppure tramite la Creazione guidata dimensione. Dopo aver definito una dimensione del database, è possibile modificare e configurare la dimensione del database in Progettazione dimensioni. È inoltre possibile personalizzare la dimensione del cubo, entro certi limiti, in Progettazione cubi.  
  
> [!NOTE]  
>  È inoltre possibile progettare e configurare dimensioni, attributi e gerarchie a livello di programmazione utilizzando XMLA o AMO (Analysis Management Objects). Per ulteriori informazioni, vedere [Analysis Services linguaggio di scripting &#40;riferimento&#41; ASSL](https://docs.microsoft.com/bi-reference/assl/analysis-services-scripting-language-assl-for-xmla) e [sviluppo con Analysis Management Objects &#40;amo ](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo)&#41;.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
 Gli argomenti disponibili in questa sezione sono descritti nella tabella seguente.  
  
 [Definire le dimensioni del database](define-database-dimensions.md)  
 Descrive come modificare e configurare una dimensione di database tramite Progettazione dimensioni.  
  
 [Riferimento alle proprietà degli attributo delle dimensioni](dimension-attribute-properties-reference.md)  
 Descrive come definire, modificare e configurare un attributo di una dimensione di database tramite Progettazione dimensioni.  
  
 [Definire relazioni tra attributi](attribute-relationships-define.md)  
 Descrive come definire, modificare e configurare una relazione tra attributi tramite Progettazione dimensioni.  
  
 [Creare gerarchie definite dall'utente](user-defined-hierarchies-create.md)  
 Descrive come definire, modificare e configurare un gerarchia definita dall'utente degli attributi di una dimensione tramite Progettazione dimensioni.  
  
 [Utilizzare la Configurazione guidata funzionalità di Business Intelligence per migliorare le dimensioni](../use-the-business-intelligence-wizard-to-enhance-dimensions.md)  
 Descrive come ottimizzare una dimensione di database mediante la Configurazione guidata funzionalità di Business Intelligence.  
  
## <a name="see-also"></a>Vedere anche  
 [Cubi nei modelli multidimensionali](cubes-in-multidimensional-models.md)  
  
  
