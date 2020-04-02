---
title: Architettura di un elemento del report personalizzato | Microsoft Docs
description: Informazioni sul modo in cui l'architettura di un elemento del report personalizzato è un'estensione che consente agli sviluppatori di aggiungere funzionalità non supportate in modo nativo in RDL.
ms.date: 03/03/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: custom-report-items
ms.topic: reference
helpviewer_keywords:
- custom report items, architecture
ms.assetid: 2a88ea46-c9f8-4dd7-aad1-16de11da4f06
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 039afae1b8be540869930055e77320c27857e23d
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "80216960"
---
# <a name="custom-report-item-architecture"></a>Architettura di un elemento del report personalizzato
  Un elemento del report personalizzato è un'estensione di RDL (Report Definition Language) che consente agli sviluppatori di aggiungere funzionalità per le quali non è disponibile il supporto nativo in RDL o di estendere le funzionalità dei controlli esistenti. Un elemento del report personalizzato è costituito da due componenti principali: il componente della fase di esecuzione e quello della fase di progettazione. Questi componenti vengono implementati come assembly [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] e possono essere scritti in qualsiasi linguaggio conforme a CLS.  
  
## <a name="the-run-time-component"></a>Componente della fase di esecuzione  
 Il componente della fase di esecuzione per un elemento del report personalizzato viene chiamato da Elaborazione report in fase di esecuzione. Questo componente accetta i dati passati da Elaborazione report in fase di esecuzione, elabora tali dati e restituisce un'immagine contenente l'elemento del report personalizzato di cui è stato eseguito il rendering.  
  
 ![Componente della fase di esecuzione di un elemento del report personalizzato](../../reporting-services/custom-report-items/media/customreportitemrun-timecomponentarchitecture.gif "Componente della fase di esecuzione di un elemento del report personalizzato")  
  
## <a name="the-design-time-component"></a>Componente della fase di progettazione  
 Il componente della fase di progettazione consente la definizione e la modifica dell'elemento del report personalizzato nell'interfaccia di Progettazione report in [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]. Questo componente è costituito da diversi controlli secondari che definiscono l'aspetto e le proprietà dell'elemento del report personalizzato nell'ambiente di progettazione.  
  
 ![Componente della fase di progettazione di un elemento del report personalizzato](../../reporting-services/custom-report-items/media/customreportitemdesign-timecomponentarchitecture.gif "Componente della fase di progettazione di un elemento del report personalizzato")  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un componente runtime dell'elemento del report personalizzato](../../reporting-services/custom-report-items/creating-a-custom-report-item-run-time-component.md)   
 [Creazione di un componente dell'elemento del report personalizzato per la fase di progettazione](../../reporting-services/custom-report-items/creating-a-custom-report-item-design-time-component.md)   
 [Procedura: Distribuire un elemento del report personalizzato](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
  
