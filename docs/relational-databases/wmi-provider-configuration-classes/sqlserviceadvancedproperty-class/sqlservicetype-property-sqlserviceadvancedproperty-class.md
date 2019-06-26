---
title: Proprietà SqlServiceType (classe SqlServiceAdvancedProperty) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SqlServiceType Property (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServiceType property
ms.assetid: 20f1663a-9a14-4f14-8c1b-8aa133e272c3
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 440d7a0d90887d6a1bbeb9553306c5453c514d02
ms.sourcegitcommit: 20d24654e056561fc33cadc25eca8b4e7f214b1b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/25/2019
ms.locfileid: "67351583"
---
# <a name="sqlservicetype-property-sqlserviceadvancedproperty-class"></a>Proprietà SqlServiceType (classe SqlServiceAdvancedProperty)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Ottiene il tipo del servizio gestito associato alla proprietà avanzata.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.SetBoolValue(NumValue)  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SqlServiceAdvancedProperty](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) che rappresenta una proprietà avanzata.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore uint32 che specifica il tipo di servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="remarks"></a>Note  
 I possibili valori restituiti sono i seguenti:  
  
|Type|Definizione|  
|----------|----------------|  
|*1*|MSSQLSERVER è il servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|*2*|SQLSERVERAGENT è il servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent.|  
|*3*|MSFTESQL è il servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] del motore di ricerca full-text.|  
|*4*|MsDtsServer è il servizio [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .|  
|*5*|MSSQLServerOLAPService è il servizio [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .|  
|*6*|ReportServer è il servizio [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .|  
|*7*|SQLBrowser è il servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Browser.|  
|*8*|NsService è il [!INCLUDE[ssNoVersion](../../../includes/ssns-md.md)] servizio di notifica.|  
|*9*|MSSQLFDLauncher è il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servizio Utilità di avvio del Daemon filtri Full-text.|  
|*10*|SQLPBENGINE è il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servizio motore Polybase.|  
|*11*|SQLPBDMS è il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Polybase Data Movement service.|  
|*12*|MSSQLLaunchpad è il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servizio Launchpad.|  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e arresto di servizi](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
