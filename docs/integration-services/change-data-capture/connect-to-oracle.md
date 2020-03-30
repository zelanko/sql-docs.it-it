---
title: Connettersi a Oracle | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- connOra
ms.assetid: 711ac7ff-5d3d-4533-80ca-d1fecdb3048f
author: chugugrace
ms.author: chugu
ms.openlocfilehash: e745a2277a01cac3dd120af241e0ae1d7575b562
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71294751"
---
# <a name="connect-to-oracle"></a>Connettersi a Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Quando si aggiungono o modificano le tabelle utilizzate nell'istanza di CDC per la prima volta, è possibile che venga richiesto di connettersi al database Oracle. Immettere le credenziali di un utente Oracle che può accedere allo schema delle tabelle da acquisire. Immettere quanto segue nella finestra di dialogo:  
  
 **autenticazione**  
  
 Selezionare uno degli elementi seguenti:  
  
-   **Windows Authentication**: selezionare questa opzione per utilizzare le credenziali del dominio Windows correnti. È possibile utilizzare questa opzione solo se il database Oracle è configurato per l'utilizzo dell'autenticazione di Windows.  
  
-   **Oracle Authentication**: se si seleziona questa opzione, è necessario digitare il **nome utente** e la **password** dell'utente nel database Oracle a cui si effettua la connessione.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiungere tabelle a un'istanza di CDC](../../integration-services/change-data-capture/add-tables-to-a-cdc-instance.md)  
  
  
