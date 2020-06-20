---
title: Parametri Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, parameters
ms.assetid: b1bb3ea3-8097-4e76-b9c2-78a0f46a23bc
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 76a5ebe7018fdc58f02a4d2454d40f172c752c4e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059272"
---
# <a name="integration-services-parameters"></a>Parametri di Integration Services
  Per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , è possibile decidere di analizzare i [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacchetti nel computer o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] i file del pacchetto nel file System. Se si sceglie di analizzare i file nel file system, specificare il percorso della cartella che contiene i pacchetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="options"></a>Opzioni  
 **Analizza pacchetti SSIS nel computer**  
 Selezionare questa opzione per analizzare i pacchetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nel computer. Questa opzione è selezionata per impostazione predefinita.  
  
 **Analizza file pacchetti SSIS**  
 Selezionare questa opzione per analizzare i pacchetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] nel file system.  
  
 **Percorso pacchetti SSIS**  
 Individuare il percorso UNC o locale in cui sono memorizzati i pacchetti [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Non è necessario includere i nomi di file. Se il percorso immesso non è accessibile, non è possibile fare clic su **Avanti**. Per impostazione predefinita, il percorso è vuoto. Questo campo è abilitato solo quando si seleziona **Analizza file di pacchetto SSIS**.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di preparazione aggiornamento](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Guida di riferimento all'interfaccia utente di Preparazione aggiornamento](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
