---
description: Proprietà SqlServiceType (classe SqlService)
title: Proprietà SqlServiceType (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SqlServiceType Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SqlServiceType property
ms.assetid: dbff2968-3011-41d6-a141-52d814af0213
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 685fb402647c7a757f7a894705cf7754d696b24d
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542813"
---
# <a name="sqlservicetype-property-sqlservice-class"></a>Proprietà SqlServiceType (classe SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Ottiene il tipo del servizio gestito.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.SqlServiceType [= value]  
```  
  
## <a name="parts"></a>Parti  
 *object*  
 Oggetto della [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) che rappresenta il servizio.  
  
## <a name="property-valuereturn-value"></a>Valore proprietà/Valore restituito  
 Valore uint32 che specifica il tipo di servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="remarks"></a>Osservazioni  
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
|*9*|MSSQLFDLauncher è il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servizio Utilità di avvio del daemon filtri full-text.|  
|*10*|SQLPBENGINE è il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servizio del motore di base.|  
|*11*|SQLPBDMS è il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servizio di spostamento dati di base.|  
|*12*|MSSQLLaunchpad è il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] servizio launchpad.|  
  
## <a name="see-also"></a>Vedere anche  
 [Avvio e arresto di servizi](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
