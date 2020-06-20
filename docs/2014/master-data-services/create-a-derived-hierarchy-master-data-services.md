---
title: Creare una gerarchia derivata (Master Data Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
helpviewer_keywords:
- derived hierarchies, creating
- creating derived hierarchies [Master Data Services]
ms.assetid: fec653c4-11cc-46a2-8dd8-b605341ebb40
author: lrtoyou1223
ms.author: lle
ms.openlocfilehash: 7c831ab360f2cbe4b32834ae2a280b961d2bac1e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84971871"
---
# <a name="create-a-derived-hierarchy-master-data-services"></a>Creare una gerarchia derivata (Master Data Services)
  In [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)]creare una gerarchia derivata quando si desidera una gerarchia basata su livelli tramite cui viene assicurato il posizionamento dei membri al corretto livello. Le gerarchie derivate sono basate sulle relazioni tra attributi basati su dominio che esistono in un modello.  
  
> [!NOTE]  
>  Se non esiste un valore di attributo basato su dominio per un determinato membro, tale membro non verrà incluso nella gerarchia derivata. Vedere [Richiedere valori di attributo &#40;Master Data Services&#41;](require-attribute-values-master-data-services.md) per richiedere un valore di attributo basato su dominio per tutti i membri.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Per eseguire questa procedura:  
  
-   È necessario disporre di autorizzazione per accedere all'area funzionale **Amministrazione sistema** .  
  
-   È necessario essere un amministratore del modello. Per ulteriori informazioni, vedere [amministratori &#40;Master Data Services&#41;](../../2014/master-data-services/administrators-master-data-services.md).  
  
### <a name="to-create-a-derived-hierarchy"></a>Per creare una gerarchia derivata  
  
1.  In [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], fare clic su **Amministrazione sistema**.  
  
2.  Nella pagina **vista modelli** scegliere **Gestisci** dalla barra dei menu, quindi fare clic su **gerarchie derivate**.  
  
3.  Nella pagina **Gestione gerarchia derivata** selezionare un modello dall'elenco **Modello** .  
  
4.  Fare clic su **Aggiungi gerarchia derivata**.  
  
5.  Nella pagina **Aggiungi gerarchia derivata** digitare un nome per la gerarchia nella casella **Nome gerarchia derivata** .  
  
    > [!TIP]  
    >  Usare un nome che descriva i livelli della gerarchia, ad esempio **Prodotto-Subcategoria-Categoria**.  
  
6.  Fare clic su **Salva gerarchia derivata**.  
  
7.  Nel riquadro **entità e gerarchie disponibili** della pagina **Modifica gerarchia derivata** fare clic su un'entità o una gerarchia e trascinarla nel riquadro **livelli correnti** .  
  
8.  Continuare a trascinare entità o gerarchie fino a che la gerarchia non è completa.  
  
9. Fare clic su **Indietro**.  
  
## <a name="see-also"></a>Vedere anche  
 [Gerarchie derivate &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-master-data-services.md)   
 [Gerarchie derivate con estremità esplicite &#40;Master Data Services&#41;](../../2014/master-data-services/derived-hierarchies-with-explicit-caps-master-data-services.md)   
 [Attributi basati su dominio &#40;Master Data Services&#41;](../../2014/master-data-services/domain-based-attributes-master-data-services.md)  
  
  
