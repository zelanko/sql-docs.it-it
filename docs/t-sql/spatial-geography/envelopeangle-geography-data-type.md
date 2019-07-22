---
title: EnvelopeAngle (tipo di dati geography) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- EnvelopeAngle
- EnvelopeAngle_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- EnvelopeAngle method
ms.assetid: 14a7ba15-168c-4b08-ba3d-951d73092ac7
author: MladjoA
ms.author: mlandzic
ms.openlocfilehash: e3289956dd79c852eef6534ad1f72623ad4dcaa6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68066458"
---
# <a name="envelopeangle-geography-data-type"></a>EnvelopeAngle (tipo di dati geography)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Restituisce l'angolo massimo, espresso in gradi, tra il punto restituito dal metodo `EnvelopeCenter()` e un punto nell'istanza **geography**.  
  
 Questo metodo con tipo di dati **geography** supporta le istanze **FullGlobe** o le istanze spaziali con dimensioni maggiori di un emisfero.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
EnvelopeAngle( )  
```  
  
## <a name="return-types"></a>Tipi restituiti  
 Tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituito: **float**  
  
 Tipo CLR restituito: **SqlDouble**  
  
## <a name="remarks"></a>Remarks  
 Questo metodo restituisce un punto nell'istanza **geography** espresso in gradi. Se usato con EnvelopeCenter(), `EnvelopeAngle()` restituisce un cerchio di delimitazione di un'istanza **geography**.  
  
 In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] questo metodo è stato esteso alle istanze **FullGlobe**.  
  
 La limitazione di emisfero applicata a `EnvelopeAngle()` in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] è stata rimossa. Tuttavia, per le istanze con angoli più ampi di 90 gradi, verrà restituito 180 gradi. `EnvelopeAngle()` non è preciso per le istanze **geography** estese a più di un emisfero.  
  
## <a name="examples"></a>Esempi  
  
```  
DECLARE @g geography = 'LINESTRING(-120 45, -120 0, -90 0)';   
SELECT @g.EnvelopeAngle();  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Metodi estesi sulle istanze di geografia](../../t-sql/spatial-geography/extended-methods-on-geography-instances.md)   
 [EnvelopeCenter &#40;tipo di dati geography&#41;](../../t-sql/spatial-geography/envelopecenter-geography-data-type.md)  
  
  
