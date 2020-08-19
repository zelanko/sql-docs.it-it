---
description: Colonne dimensioni a modifica lenta (Configurazione guidata dimensioni a modifica lenta)
title: Colonne dimensioni a modifica lenta (Configurazione guidata dimensioni a modifica lenta) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.loaddimwizard.scdsupport.f1
ms.assetid: 36de99d5-5368-48e0-b876-17e9c6862c6c
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 8b27c9c0e575775449d2f3a25c5a20bd6667b5cd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88425723"
---
# <a name="slowly-changing-dimension-columns-slowly-changing-dimension-wizard"></a>Colonne dimensioni a modifica lenta (Configurazione guidata dimensioni a modifica lenta)

[!INCLUDE[sqlserver-ssis](../../../includes/applies-to-version/sqlserver-ssis.md)]


  Utilizzare la finestra di dialogo **Colonne dimensioni a modifica lenta** per selezionare un tipo di modifica per ogni colonna delle dimensioni a modifica lenta.  
  
 Per ulteriori informazioni su questa procedura guidata, vedere [Slowly Changing Dimension Transformation](../../../integration-services/data-flow/transformations/slowly-changing-dimension-transformation.md).  
  
## <a name="options"></a>Opzioni  
 **Colonne dimensione**  
 Consente di selezionare una colonna nell'elenco.  
  
 **Tipo di modifica**  
 Consente di selezionare un **Attributo fisso**o uno dei due tipi di attributi modificabili. Utilizzare **Attributo fisso** quando il valore di una colonna non deve cambiare. Le modifiche verranno trattate come errori in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] . Utilizzare **Attributo modificabile** per sovrascrivere i valori esistenti con i valori modificati. Utilizzare **Attributo cronologico** per salvare i valori modificati in nuovi record, contrassegnando contemporaneamente i record precedenti come obsoleti.  
  
 **Rimuovi**  
 Consente di selezionare una colonna delle dimensioni e di rimuoverla dall'elenco di colonne mappate facendo clic su **Rimuovi**.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurazione degli output tramite Configurazione guidata dimensioni a modifica lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
