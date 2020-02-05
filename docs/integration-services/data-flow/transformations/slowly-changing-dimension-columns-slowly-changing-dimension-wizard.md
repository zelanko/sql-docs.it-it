---
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
ms.openlocfilehash: 945a9b23fd9f5850489184d89d99d4ae24350652
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71291209"
---
# <a name="slowly-changing-dimension-columns-slowly-changing-dimension-wizard"></a>Colonne dimensioni a modifica lenta (Configurazione guidata dimensioni a modifica lenta)

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
 [Configurare gli output tramite Configurazione guidata dimensioni a modifica lenta](../../../integration-services/data-flow/transformations/configure-outputs-using-the-slowly-changing-dimension-wizard.md)  
  
  
