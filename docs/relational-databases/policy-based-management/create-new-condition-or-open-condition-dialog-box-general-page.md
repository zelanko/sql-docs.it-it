---
title: Finestra di dialogo Crea nuova condizione o Apri condizione, pagina Generale | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
f1_keywords:
- sql13.swb.dmf.condition.f1
ms.assetid: 106954bf-e4ba-412b-9c1a-907d06153dcd
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 7c5c0a596b943724ccfedc9dc2e1dec57f6c0520
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63009852"
---
# <a name="create-new-condition-or-open-condition-dialog-box-general-page"></a>Finestra di dialogo Crea nuova condizione o Apri condizione, pagina Generale
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilizzare questa finestra di dialogo per creare o modificare una condizione della gestione basata su criteri. Una condizione è un'espressione booleana che specifica un set di stati consentiti per una destinazione gestita della gestione basata su criteri in relazione ai facet. Le proprietà che è possibile selezionare nella casella **Espressione/Campo** variano a seconda del facet usato. Per altre informazioni sulla correlazione delle condizioni con facet e criteri, vedere [Amministrazione di server tramite la gestione basata su criteri](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md).  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Per una nuova condizione, digitare il relativo nome. Per una condizione esistente, il nome è già visualizzato.  
  
 **Facet**  
 Facet utilizzato dalla condizione.  
  
 **AndOr**  
 Quando si aggiungono più espressioni, indica se queste devono essere unite in join tramite **And** o **Or**. Se è disponibile un'unica espressione, il campo rimane vuoto.  
  
 **Campo**  
 Ogni facet espone una o più proprietà che è possibile impostare. Nella casella del campo, effettuare una selezione dall'elenco di proprietà disponibili per creare un'espressione per questa condizione.  
  
 **Operatore**  
 Selezionare un operatore di confronto per l'espressione. Gli operatori sono i seguenti: =! = >, >= <, <=, [NOT]LIKE, [NOT]IN. Per alcune proprietà non sono disponibili tutti gli operatori.  
  
 **Value**  
 Impostazione del valore per l'espressione. I valori consentiti dipendono dal facet. I valori possono essere TRUE/FALSE, di tipo stringa o numerico. I valori stringa devono essere racchiusi tra virgolette singole, ad esempio: **'AdventureWorks'** . Per alcune proprietà non sono disponibili tutti gli operatori.  
  
## <a name="group-clauses"></a>Raggruppa clausole  
 Le clausole possono essere raggruppate in modo che funzionino come un'unità singola separata dal resto della query, in modo analogo all'utilizzo di parentesi per racchiudere un'espressione in un'equazione matematica o in un'istruzione logica. Il raggruppamento delle clausole è utile quando si compilano query complesse.  
  
 **Per raggruppare le clausole**  
  
-   Premere MAIUSC o CTRL, quindi fare clic su due o più clausole per selezionare un intervallo. Fare clic con il pulsante destro del mouse sull'area selezionata, quindi scegliere **Raggruppa clausole**.  
  
## <a name="see-also"></a>Vedere anche  
 [Amministrazione di server tramite la gestione basata su criteri](../../relational-databases/policy-based-management/administer-servers-by-using-policy-based-management.md)  
  
  
